# Mailjet GraphQL Schema

## Overview

This conceptual GraphQL schema models the Mailjet Email API (v3), covering the full surface of Mailjet's REST API at https://dev.mailjet.com/email/reference/. The schema represents email sending, contact management, campaign management, statistics, webhooks, inbound email parsing, and account administration.

## Source

- API Reference: https://dev.mailjet.com/email/reference/
- Developer Documentation: https://dev.mailjet.com/email/guides/
- Base URL: https://api.mailjet.com/v3

## Schema File

See `mailjet-schema.graphql` for the full type definitions.

## Type Summary

| Category | Types |
|---|---|
| Messaging | Message, MessageDetails, MessageStatus, EmailMessage, EmailDetails, EmailHeader |
| Recipients | Recipient, RecipientDetails |
| Contacts | Contact, ContactDetails, ContactEmail, ContactProperties |
| Lists | ContactList, ListMember, ListMembership, ContactsListMembership |
| Campaigns | Campaign, CampaignDetails, CampaignDraft, CampaignDraftDetails, CampaignDraftStatus, CampaignStatistics |
| Templates | Template, TemplateDetails, TemplateContent |
| Senders | Sender, SenderDetails |
| Domains | Domain, DomainDetails, SPF, DKIM |
| Statistics | Statistics, DeliveryStats, OpenStats, ClickStats, BounceStats, UnsubscribeStats, SpamStats |
| Suppressions | Suppression, SuppressionDetails |
| Bulk Jobs | BulkJob, BulkJobDetails, BulkJobStatus |
| Webhooks | Webhook, WebhookDetails, WebhookEvent |
| Inbound Email | ParseRoute, InboundEmail, InboundDetails |
| Account | SubAccount, APIKey, SecretKey, Token |

## Key Queries

- `message(id: ID!)` — Retrieve a single message by ID
- `messages(limit: Int, offset: Int, status: MessageStatusEnum)` — List messages with filtering
- `contact(id: ID!)` — Look up a contact
- `contacts(limit: Int, offset: Int)` — Paginated contact list
- `contactList(id: ID!)` — Retrieve a contact list
- `campaign(id: ID!)` — Get campaign details
- `campaignDraft(id: ID!)` — Get a draft campaign
- `template(id: ID!)` — Retrieve a template
- `sender(id: ID!)` — Look up a validated sender
- `statistics(campaignID: ID, fromTS: String, toTS: String)` — Aggregated delivery statistics
- `webhooks` — List all configured event webhooks
- `parseRoutes` — List inbound email parse routes

## Key Mutations

- `sendEmail(input: SendEmailInput!)` — Send a transactional email
- `createContact(input: CreateContactInput!)` — Create a new contact
- `updateContact(id: ID!, input: UpdateContactInput!)` — Update contact properties
- `subscribeContactToList(contactID: ID!, listID: ID!)` — Add contact to a list
- `unsubscribeContactFromList(contactID: ID!, listID: ID!)` — Remove contact from list
- `createCampaignDraft(input: CreateCampaignDraftInput!)` — Create a draft campaign
- `sendCampaignDraft(id: ID!)` — Trigger sending of a draft campaign
- `createTemplate(input: CreateTemplateInput!)` — Create an email template
- `addSender(input: AddSenderInput!)` — Register a sender address
- `createWebhook(input: CreateWebhookInput!)` — Register a webhook endpoint
- `createParseRoute(input: CreateParseRouteInput!)` — Register an inbound parse route
- `addToSuppressionList(input: SuppressionInput!)` — Suppress an email address
- `createBulkJob(input: BulkJobInput!)` — Submit a bulk contact import job

## Authentication

Mailjet uses HTTP Basic Authentication with the API Key as the username and Secret Key as the password. This schema models those credentials as `APIKey` and `SecretKey` types within the account administration section.

## Pagination

All list queries follow Mailjet's REST API pagination model with `limit` and `offset` integer arguments, and return a `total` count alongside the data array.
