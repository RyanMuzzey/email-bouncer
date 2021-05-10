# email-bouncer Concept

## Problem
Our personal email addresses are often leaked by the third parties we trust them with, exposing them and potentially other personal data to the open market. We often share our email addresses among different sites, increasing the potential impact of such leaks, and our exposure to spam. Ideally, each web site we trust our email addresses with would be given a unique address which wouldn't be shared with other sites. Additionally, each of these addresses would have a single valid origin for emails, enabling them to reject all incoming mail from unknown origins.

## Idea
Create a service which can:
1. Enable you to create and manage unique, single-use email addresses.
2. Forward emails to configured back-end email addresses if the sender to the unique address is expected, and bounce the rest.

![Design diagram. Expected emails are forwarded to back-end addresses while unexpected ones are discarded.](https://github.com/RyanMuzzey/email-bouncer/raw/main/docs/EmailBouncer.png)

## Impact
* 100% less spam or unwanted email. All emails forwarded by the system are from approved senders.
* Reduced impact of third party data leaks. Third parties no longer have your real email address so any leaks won’t result in more unwanted mail.

## Customers
* Email user - People who need secure, spam free, email addresses.
* Manager - People who need to manage the email mappings and set up new addresses.
* Admin - People who need to manage the email system infrastructure.
* Bill payer - People who need to keep up with the cost of the system and pay bills. 

## Use Cases
1. As an email user, I want to be able to create unique email addresses so that I can receive email.
1. As an email user, I want to be able to map a unique email address to a single sender so that I can filter emails based on the sender.
1. As an email user, I want to be able to map unique email addresses to a back-end email address so I know who to forward emails to.
1. As an email user, I want to be able to forward emails which get past the filters on to back-end email addresses.
1. As an email user, I want my data to be securely stored.
1. As an email user, I want my data to be isolated from the outside world.
1. As a manager, I want to be able to update and delete my unique and back-end email records.
1. As an admin, I want to be able to scale my cloud resources to handle my email workload.
1. As an admin, I want to be able to view a performance dashboard so that I know can stay informed on how the service is operating.
1. As a bill payer, I want to be able to view an estimate of my monthly cost so that I know how much my current capacity will cost over the month.
1. As a bill payer, I want to be able to download itemized statements of my current costs so that I can determine how much I paid for my capacity over a period of time I specify.

## Requirements

| As a...  | I want to... | So that... | Priority | Use Case |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|
| Email user      | Be able to bring my own email domain to bouncer | My unique email addresses are valid for receiving email | P0 | UC1 |
|  | Generate unique, 8 character long, email addresses | Use them to receive emails | P0 | UC1 |
| | Store the unique email addresses | They can be used to receive emails | P0 | UC1 |
| | Store back-end email addresses | They can be used as email forwarding destinations | P0 | UC1 |
| | Associate a single valid sender for each unique email address | Any emails originating from an invalid sender will be filtered out, and not forwarded to a back-end email address | P0 | UC2 |
| | Break the association between a unique email address and a valid sender | Stop receiving emails from a sender | P0 | UC2 |
| | Associate a back-end email address with each unique email address | Any emails not filtered out can be forwarded to the associated back-end email address | P0 | UC3 |
| | Forward valid emails to the correct back-end email address | Receive valid emails at the back-end email address | P0 | UC4 |
| | Have the sender and unique email associations encrypted in storage | I can limit the risk of unauthorized senders sending emails through the filters | P0 | UC5 |
| | Have the back-end email addresses securely encrypted in storage | I can limit the risk of the destination email addresses being leaked, defeating the purpose of the system | P0 | UC5 |
| | Have any data stored in the system not flow out of the system | I know that my data is only used internally and has no egress from the system | P0 | UC6 |
| Manager | Have a user interface to create, update, and delete unique addresses, their associated sender addresses, and back-end addresses | I have a simple way to manage my data | P1 | UC7 |
| | Be able to view a listing of my unique, sender, and back-end addresses which can be paged through, sorted, and filtered | I can view my data at a glance, and drill down to what I’m looking for | P1 | UC7 |
| Admin | Be able to scale the infrastructure of the service | It meets my needs for performance and cost | P2 | UC8 |
| | Be able to view a dashboard of the availability and latency in the service | I can make informed decisions based on the current status of the system | P2 | UC9 |
| Bill Payer | Be able to view an estimate of my monthly costs for the currently configured infrastructure | I have an idea of what my monthly bill could be | P2 | UC10 |
| | Be able to download itemized statements | I know where money is being spent in the service | P2 | UC11 |

## Components
* Email filtering and delivery
* Secure storage for the data
* Front-end to manage the email addresses and associated data

## Tenets
* Data security is a primary concern.
* Use the right tool for the task

## FAQ
### Is email bouncer a mailbox?
No, you must bring your own destination email and the system will forward mail there.

### Is my email being opened?
No, the system only looks at the sender before discarding the message or forwarding it to your specified email address.

### Are email domains provided?
No, you must register and bring your own web domain.

# Links
* [SES - forward incoming email to external address](https://aws.amazon.com/blogs/messaging-and-targeting/forward-incoming-email-to-an-external-destination/)
* [SendGrid - Alternative using webhooks](https://sendgrid.com/docs/ui/account-and-settings/inbound-parse/)
