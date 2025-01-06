# Time to process logins Asp.net 8.md

I have started reading the book [Advanced ASP.NET Core 8 Security: Move Beyond ASP.NET Documentation and Learn Real Security](https://link.springer.com/book/10.1007/979-8-8688-0494-6) by Scott Norberg.
See also [amazon link](https://www.amazon.com/Advanced-ASP-NET-Core-Security-Documentation/dp/B0D5TX37HY).


Different from the most security books' authors, Scott Norberg knows how to code and his knowledge shines in the book.

Highly suggested for any senior software .Net developer.

I am reading the chapter for Authentication and Authorization.
There is a very interesting figure in the book which you can see below:

![process-time-logins](./images/process-time-logins.png)


This figure shows the processing time when you try to login to asp.net site for existing users and not existing users.
This is due to fact that if a user does not exists asp.net immediately returns from the call.
Implementation could be seen in [CheckPassword method of UserManager](https://github.com/dotnet/aspnetcore/blob/v8.0.11/src/Identity/Extensions.Core/src/UserManager.cs#L675).

This means that an attacker will be able to guess existing usernames with a little bit effort.

The author, Scott Norberg, summarizes this very well.
You might have learned that minimizing server processing is always the right approach. 
However, I want to highlight that this principle can sometimes be detrimental to security.


This is what I like about this book.
Scott Norberg is clearly aware of trade-offs between security and UX, security and performance.
Not everyone is.




