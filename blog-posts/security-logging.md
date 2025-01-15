Panel and Security logging

A video named [Panel](https://youtu.be/5BzGetrwpoU) by  140journos in youtube is published yesterday, in Jan 14, 2025.
It is viewed by 983692 times in one day only when I am writing this sentences.
Video description is below:

>What could be worse than the state's most confidential data falling into the hands of 15-year-old teenagers? 
>That data falling into the hands of bad brothers.

>A very simple security vulnerability discovered in e-nabız in the summer of 2022 caused the data of 101 million people to be spilled, igniting an unstoppable chaos.

>An illegal market built on stolen data...

e-nabız, a system from Health Ministry, stores a lot of confidential information about Turkish Citizens and those who use Turkish hospitals.

The simple security vulnerability is described in 22:50 of 25 minutes of video.
[See here](https://youtu.be/5BzGetrwpoU?t=1370).

According to video, when you want to reset your password, system sends you a code via SMS for reset confirmation.
But again according to video, developers logged this information in frontend using javascript.
This information also included SMS code itself.
Therefore, writing a script these attackers was able to gain access to system.
Again, according to video, they used distributed attack from two Turkish cities, Adana and İstanbul, to gain a lot a lot of confidential information.

I do not want to talk about if this attack is occurred or not.
I also do not want to talk about what the Turkish government should do.

But I want to talk about the security perspective of this attack from a developer side.

First of all, of course, such a sensitive information should not be logged in the client side.
But a lot of developers are becoming less knowledgeable in fundamentals, thus, less knowledgeable in security also.
See this [video Web Developers Are Disconnected](https://www.youtube.com/watch?v=oNjfXnhq0UM) and this blog post [How do you do, fellow web developers? A growing disconnect](https://rakhim.exotext.com/web-developers-a-growing-disconnect).

> I had a "woah" moment once when one programmer got genuinely baffled about the fact that a website somehow "erases" the history of requests from the Network tab of Chrome DevTools. He was wondering what magic method was used to hide the communication. He hadn't realized the app was not a single-page JS application (SPA), and he actually wasn't aware there is another way to make web apps. The idea that each click actually makes the browser fetch a completely new page, without any JS involved, was alien to him. 

This web developer was  unaware of multi page application, an application type which existed from dawn of internet.
How could you expect security knowledge from this developer.

I digress, I would like to talk about Chapter 11 Logging and Error Handling of the book [Advanced ASP.NET Core 8 Security: Move Beyond ASP.NET Documentation and Learn Real Security](https://link.springer.com/book/10.1007/979-8-8688-0494-6) by Scott Norberg.

Norberg starts talking what to log and what not to log.
For example, in the logging and compliance part, he talks about logging who accessed the sensitive information.

Then he talks about .NET logging but rightly assert that it is developer focused not security focused.

He proposes logging a lot of information.
These include following, see the book or [the code](https://github.com/Apress/Advanced-ASP.NET-Core-8-Security-2nd-ed) for complete list.

- Event ID
- Logged-In User ID 
- Request IP Address 
- Request Path 

In the government ERP systems, I have worked before, we have logged very similar information also.
Logged-in User ID is a very useful information to have.

But he also proposes adding these two critical attributes.

- SecurityEventType
- SecurityLevel

Below code examples are taken from [book github repo, JuiceShopDotNet.Safe/Logging folder](https://github.com/Apress/Advanced-ASP.NET-Core-8-Security-2nd-ed/tree/main/JuiceShopDotNet.Safe/Logging)



```csharp
public enum SecurityLevel
{
    SECURITY_NA = 1,
    SECURITY_SUCCESS = 2,
    SECURITY_AUDIT = 3,
    SECURITY_INFO = 4,
    SECURITY_WARNING = 5,
    SECURITY_ERROR = 6,
    SECURITY_CRITICAL = 7
}
```

Here, whenever you log something in the backend, you also log also SecurityLevel.

He gives an example, SecurityEvent Authentication, for log on pages.

```csharp
public static partial class SecurityEvent
{
    public static class Authentication
    {
        public static SecurityEventType LOGIN_SUCCESSFUL { get; } = new SecurityEventType(1200, LogLevel.Information, SecurityEventType.SecurityLevel.SECURITY_SUCCESS);
        public static SecurityEventType LOGOUT_SUCCESSFUL { get; } = new SecurityEventType(1201, LogLevel.Information, SecurityEventType.SecurityLevel.SECURITY_SUCCESS);
        public static SecurityEventType PASSWORD_MISMATCH { get; } = new SecurityEventType(1202, LogLevel.Debug, SecurityEventType.SecurityLevel.SECURITY_INFO);
        public static SecurityEventType USER_LOCKED_OUT { get; } = new SecurityEventType(1203, LogLevel.Debug, SecurityEventType.SecurityLevel.SECURITY_WARNING);
        public static SecurityEventType USER_NOT_FOUND { get; } = new SecurityEventType(1204, LogLevel.Information, SecurityEventType.SecurityLevel.SECURITY_WARNING);
        public static SecurityEventType LOGIN_SUCCESS_2FA_REQUIRED { get; } = new SecurityEventType(1210, LogLevel.Information, SecurityEventType.SecurityLevel.SECURITY_INFO);
    }
}
```

So far so good. 
In my systems, I am also logging EventId for tracking user problems.
How this SecurityEvent and SecurityLevel will help me?

Author calls this **Using Logging in Your Active Defenses**
Author advises to store logs in database for easy querying and using this security information for active defenses.

Since the system logs, SecurityEventType and SecurityLevel information, our system code can check these information in active defenses.
Following examples are from book:

- check the number of times a user from a particular IP tried to log in and their password did not work. If this count is higher than 20, block that user from reaching the page for a time.

- if particular user tried to reset 5 times in the same day, prevent that user from resetting for a while.


See the example code below for this two use cases.

```csharp
private bool CanAccessPage()
    {
        var sourceIp = HttpContext.Connection.RemoteIpAddress.ToString();

        //SqlQuery is smart enough to understand that interpolated string values should be treated as parameters, so this is safe from SQL injection attacks
        var failedUsernameCount = _dbContext.Database.SqlQuery<int>($"SELECT COUNT(1) AS Value FROM SecurityEvent WHERE DateCreated > {DateTime.UtcNow.AddDays(-1)} AND RequestIP = {sourceIp} AND EventID = {Logging.SecurityEvent.Authentication.USER_NOT_FOUND.EventId}").Single();

        var failedPasswordCount = _dbContext.Database.SqlQuery<int>($"SELECT COUNT(1) AS Value FROM SecurityEvent WHERE DateCreated > {DateTime.UtcNow.AddDays(-1)} AND RequestIP = {sourceIp} AND EventID = {Logging.SecurityEvent.Authentication.PASSWORD_MISMATCH.EventId}").Single();

        if (failedUsernameCount >= 5 || failedPasswordCount >= 20)
            return false;
        else
            return true;
    }
```  
Current example code does not have this functionality but IP based restrictions without user information could also be added to these active defenses.
Such defenses would have prevented this described e-nabız attack in the back end  even with problematic frontend code.




