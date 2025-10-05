###### Introduction
- AWS Organization is a service that lets you **centrally manage multiple** AWS accounts.
- Instead of managing everything in one account, you can group accounts and apply policies, billing and governance across all of them.
- It's especially *useful for enterprises* that need separate accounts for dev, test, prod, security, billing, etc.
###### Key Features of AWS Organizations:
- Multi-account management -> Create and manage many AWS accounts from one place.
- Consolidated billing -> Get a single bill for all accounts in the organization.
- [[Service Control Policies (SPCs) ]]->Apply organization-wide permission guardrails. 
- Organizational Unit (OUs) -> Group accounts logically (e.g. by department, environment).
- Delegated administration -> Assign specific accounts to manage certain AWS services across the org.
- Integration with AWS security services -> AWS Config, GuardDuty, Security Hub can be enabled org-wide.

###### Organization Structure:

[ Management Account ]
        │
        ├── [ OU: Development ]
        │        ├── Account A
        │        ├── Account B
        │
        ├── [ OU: Production ]
        │        ├── Account C
        │        └── Account D
        │
        └── [ OU: Security ]
                 ├── Logging Account
                 └── Audit Account
 - Management account (formerly master) -> The central controlling account
 - Member accounts -> Other accounts that join the org.
 - OUs (Organizational Units) -> Like folders to group accounts.

Basic Video Lecture:
[https://www.youtube.com/watch?v=bQ2EtLnN6KQ]()

#flashcards
