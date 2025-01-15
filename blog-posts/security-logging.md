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
Logged in user ID is very useful information to have.

But he also proposes adding these two critical information.

- SecurityEventType
- SecurityLevel


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






When I watched this video, I remembered my recently



