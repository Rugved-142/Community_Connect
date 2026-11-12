# Community Connect

A Java Swing desktop application for coordinating a volunteer and donation network. Built as a group project for INFO 5100 (Group 33) at Northeastern University.

All data is held in memory and regenerated on every launch. There is no database.

## What it does

The app models a four-level hierarchy: **Network → Enterprise → Organization → Users**. On startup it builds four enterprises and six organizations:

| Enterprise | Organizations |
|---|---|
| Non-Profit Enterprise | Volunteer Management, Aid Distribution |
| Corporate Donors Enterprise | Campaign Management, Analytics & Reporting |
| Public Service Enterprise | Recipient Registration |
| Community Support Enterprise | Donation Management |

There are eight user roles, each with its own screens: system administrator, aid coordinator, volunteer coordinator, volunteer, donor, aid recipient, campaign organizer and data analyst.

Main areas:

- **Volunteers:** coordinators and administrators view and manage volunteers, and coordinators can text a selected volunteer (see SMS below).
- **Donations:** donors give through the app and organizations record each donation.
- **Campaigns:** campaign records are managed from the administrator and organizer screens.
- **Aid:** recipients register, submit aid requests and view their request history. Administrators and aid coordinators work with requests and a resource inventory.
- **Reports:** data analysts have report screens, including a resources report.

## Sample data

At launch, `DataConfiguration/ConfigureNetwork.java` generates sample data with JavaFaker: 48 volunteers, 30 aid recipients, 20 data analysts and 24 campaigns, plus a few named sample accounts and two sample donations. No aid requests are created in advance.

## Run it

Requirements: JDK 21 and Maven 3.6 or newer.

```bash
mvn clean compile
mvn exec:java
```

The main class is `ui.MainJFrame`, set in `pom.xml`.

Demo sign-in: `admin@admin.com` with the password `password`. Generated accounts also use the password `password`. See `ConfigureNetwork.java` for how each role's username is created.

## SMS (optional)

Twilio SMS is used in one place: the volunteer coordinator dashboard can send a text message to a selected volunteer. To enable it, create a `.env` file in the project root:

```env
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_ACCOUNT_TOKEN=your_auth_token
```

Then set your Twilio sending number in `SMSFeature/SmsSender.java`. Without these, the app runs normally and only sending an SMS fails.

## Project structure

```
src/main/java/
├── AidRequest/          Resource inventory and distribution status
├── Campaign/            Campaign model
├── DataConfiguration/   Network, enterprise and organization classes, and sample data setup
├── Directories/         Enterprise and organization directories
├── SMSFeature/          Twilio SMS sender
├── model/               Users, profiles and organization entities
└── ui/                  Swing screens: login, registration, admin, aid, donations, analytics
```

## Design documents

The repository includes the project proposal, class diagram, component diagram and the final presentation:

- `AED_Final_Project_Proposal-Group_33.pdf`
- `ClassDiagramPDF.pdf`
- `ComponentDiagramPDF.pdf`
- `INFO-5100-FinalProject-Group33.pptx`

## Limitations

- Data is not saved. Closing the app discards everything.
- There are no automated tests.
- SMS is available from one screen only and needs a Twilio account.
- The sample accounts use a shared demo password, so this is a course project and not production software.

## Team

- Sarthak Deshmukh
- Nachiket Sahare
- Rugved Gundawar
