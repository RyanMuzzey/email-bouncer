# email-bouncer Concept

## Problem
Our personal email addresses are often leaked by the third parties we trust them with, exposing them and potentially other personal data to the open market. We often share our email addresses among different sites, increasing the potential impact of such leaks, and our exposure to spam. Ideally, each web site we trust our email addresses with would be given a unique address which wouldn't be shared with other sites. Additionally, each of these addresses would have a single valid origin for emails, enabling them to reject all incoming mail from unknown origins.

## Idea
Create a service which can:
1. Enable you to create and manage unique, single-use email addresses.
2. Forward emails to configured back-end email addresses if the sender to the unique address is expected, and bounce the rest.

![Design diagram. Expected emails are forwarded to back-end addresses while unexpected ones are discarded.](https://github.com/RyanMuzzey/email-bouncer/raw/main/docs/EmailBouncer.png)

