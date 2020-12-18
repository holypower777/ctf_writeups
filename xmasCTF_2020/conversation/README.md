# Conversation (50 points)

## Description

Due to our company's strict policy, all chatting websites have been blocked. We have been informed that some of our employees managed to circumvent all our limitations and have a secret conversation - can you find out what they've talked about?

Author: yakuhito

[Attached file](logs.pcapng)

## Solution

I found a TCP packet in which base64 was. Following the TCP packet, we see the following dialog:

```
Hello there, yakuhito
Hello, John! Nice to hear from you again. It's been a while.
I'm sorry about that... the folks at my company restrict our access to chat apps.
Do you have it?
Have what?
The thing.
Oh, sure. Here it comes:
JP1ADIA7DJ5hLI9zpz9gK21upzgyqTyhM19bLKAsLI9hMKqsLz95MaWcMJ5xYJEuBQR3LmpkZwx5ZGL3AGS9Pt==
Doesn't look like the thing
A guy like you should know what to do with it.
May I get a hint? :)
rot13
Got it. Thanks.
```

Flag: X-MAS{Anna_from_marketing_has_a_new_boyfriend-da817c7129916751}