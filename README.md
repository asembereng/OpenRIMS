<img src="Logos/MTaPS_Name%2BUSAID.Horz.png" width="150"> &nbsp;&nbsp; <img src="Logos/MSH_4c.png" width="75"> &nbsp;&nbsp; <img src="logos/LogoOpenRIMSnew450x450-e1658854010600.png" width="45">

# OpenRIMS

> The MTaPS Project is funded by the U.S. Agency for International Development (USAID) under contract no. 7200AA18C00074 and implemented by Management Sciences for Health. The information provided on this web site is not official U.S. Government information and does not represent the views or positions of the U.S. Agency for International Development or the U.S. Government.

OpenRIMS is the next-generation software platform to assist **National Medicines Regulatory Authorities (NMRAs)** in their routine tasks. It allows the creation of country-specific software installations without re-programming. Rich configuration features allow customizing data structures, workflows, document templates, and reports.

---

## Table of Contents
- [Implemented Features](#implemented-features)
- [In Progress / Planned Features](#in-progress--planned-features)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Contact](#contact)
- [License & Disclaimer](#license--disclaimer)

---

## Implemented Features

### Application & Registration Management

OpenRIMS provides a complete end-to-end lifecycle for medicine and product registration. Applicants can start a new registration submission (`ApplicationStart`), select an existing application to continue working on (`ApplicationSelect`), and track its progress through all review stages. The system stores all application data (`ApplicationData`), attached supporting documents (`ApplicationFiles`), and assigned register numbers (`Register`) in a single record. Regulators manage active submissions through the **Activity Manager** (`ActivityManager`), which presents the assigned reviewer with the application's current checklist, data form, history, and available routing actions (submit, return to applicant, reject) on one screen.

- **Full application lifecycle** – New submissions, in-progress tracking, approval, and post-approval management for any product category, all within a configurable workflow.
- **Configurable checklists** (`CheckList`) – Each workflow activity can carry a Yes/No/N/A checklist that reviewers must complete before routing the application to the next stage. Checklist items are dictionary-driven and fully configurable by administrators.
- **Amendment management** – Regulators and applicants can open a post-approval amendment workflow (`AmendmentSelect`, `AmendmentAdd`, `AmendmentActivity`) to modify approved registrations without losing the original record.
- **Renewal management** – Separate renewal workflow (`RenewSelect`) allows re-evaluation of registrations nearing expiry, with automatic link to the original approval.
- **De-registration** – Formal withdrawal workflow (`DeRegistrationSelect`, `DeregistrationAdd`) that tracks the reason and date of de-registration while preserving the full history.
- **Inspection management** (`InspectionSelect`) – Standalone inspection workflow that can be triggered independently of product registration, supporting site audits and GMP inspections.
- **Application event log** (`ApplicationEvents`, `ApplicationEventData`) – Every state transition and user action on an application is recorded and displayed as a chronological event log for full traceability.
- **Application history & register numbers** – Registration number assignment (`Register`) with configurable validity periods and expiry dates; all previously assigned numbers are browsable from the application record (`ApplicationRegisters`).
- **Public permit viewer** (`PublicPermitData`, `PermitList`) – Approved registrations can be published to a public-facing, read-only permit list so that citizens and healthcare professionals can verify the registration status of any product without logging in.
- **Application receipt** (`SubmitReciept`) – A timestamped submission receipt can be generated and downloaded in PDF at the point of submission for the applicant's records.

---

### Workflow & Process Configuration

One of OpenRIMS' core strengths is that entire regulatory processes can be defined and modified in the UI without any code changes.

- **Process Configurator** (`ProcessConfigurator`) – Administrators select a process type from a master dictionary, then define or edit the ordered list of workflow stages (activities) using the **Workflow Configurator** (`WorkflowConfigurator`). Each stage specifies the responsible role, the data form to display, checklist items, and available routing actions. Changes take effect immediately for new applications.
- **Workflow data configurator** (`DataConfigurator`, `DataCollForm`, `DataVarTable`, `DataVarForm`) – For every workflow stage, administrators define the exact data variables (text, date, number, dropdown, file upload, address, etc.) that reviewers or applicants must fill in. Forms are previewed live before publishing (`DataFormPreview`).
- **Variable assistant** (`VariableAssistant`, `VariableAssistantEdit`) – A guided editor for creating and editing form variables, including validation rules, dictionary bindings, and display order.
- **Process validator** (`ProcessValidator`) – A built-in consistency checker that validates a workflow definition before activation, flagging missing data forms, circular routes, or unresolved references.
- **Workflow export/import** (`ImportWorkflow`, `ImportDataConfiguration`) – Completed workflow definitions can be exported to Excel and imported into another OpenRIMS instance, enabling configuration reuse across country deployments.
- **Scheduler** (`Scheduler`, `HostSchedule`) – Recurring background jobs (e.g. triggering renewal reminders, batch status checks) are attached to specific workflow stages and are configured with start date and recurrence interval directly in the application form.
- **Activity re-assignment** (`ReassignActivities`) – Supervisors can move all open activities from one employee to another in bulk, for example when a staff member is on leave. The current workload and available capacity are shown side by side.
- **Applicant user re-assignment** (`ReassignUsers`, `ReassignUsersLog`) – When an applicant changes the email/account under which their submissions were filed, a supervisor can transfer all historical and in-progress submissions to the new account. A log of all re-assignments is retained.
- **Timeline view** (`TimeLine`) – Each application displays a visual timeline of its workflow history, showing when each stage was entered, completed, and by whom.
- **To-do list** (`ToDoList`) – Every logged-in user sees a personal task queue of activities currently assigned to them, with direct links into the relevant application.

---

### Data & Dictionary Configuration

- **Dictionary management** (`Dictionaries`, `Dictionary`, `DictLevel`, `DictNode`, `RootNode`) – Hierarchical, multi-level code lists underpin all dropdown fields, workflow routing, and report categories in OpenRIMS. Administrators manage the full tree structure (add, edit, move, deactivate nodes) through a graphical tree editor. Each node stores a URL-based identifier that is used as a stable reference across configurations.
- **ATC codes** (`ATCCodes`, `Import_ATC`) – Full WHO Anatomical Therapeutic Chemical classification tree is stored and manageable within the system. Codes can be imported in bulk from a standard Excel template.
- **INN (International Non-proprietary Names)** (`Inns`) – The INN reference list used for drug substance identification is maintained in a searchable, paginated table with add/edit capabilities.
- **Excipients** (`Excipients`) – Similar to INNs, the excipient reference catalogue supports controlled vocabulary for inactive ingredient declarations.
- **Data sources configurator** (`DataSources`, `DataSource`, `DataSourceDetails`, `DataSourceTest`) – Administrators can define external SQL data sources and test their queries from inside the UI. These are used to feed lookup tables and reports from warehouse or legacy databases.
- **Formats** (`Formats`) – Country-specific date and number display formats are configurable per locale, so the same installation can present dates in DD/MM/YYYY for one country and MM/DD/YYYY for another.

---

### Monitoring & Reporting

- **Monitoring dashboard** (`Monitoring`, `MonitoringActual`, `MonitoringScheduled`, `MonitoringFullsearch`) – The monitoring module gives regulators and supervisors three complementary views:
  - *Actual* – all applications currently active (in-progress) in any workflow stage, with owner and elapsed-time information.
  - *Scheduled* – upcoming renewal and inspection deadlines, sorted by date.
  - *Full search* – a cross-workflow, cross-status search with date-range filters, allowing supervisors to find any application by applicant, product name, status, or registration number.
- **Report configurator** (`ReportConfigurator`) – Administrators define named report templates that combine application data fields, dictionary values, and date ranges. Three scopes are supported: public reports (visible without login), NMRA internal reports, and applicant-facing reports.
- **External reports** (`ReportsExternal`) – Configured reports are rendered on demand and can be exported to Excel for distribution outside the system.
- **Application history report** (`ApplicationHistory`) – A detailed, printable history of every action taken on a specific application, suitable for regulatory audits.
- **Things publisher** (`ThingsPublisher`) – Allows administrators to publish selected application data sets as structured, downloadable reports for external stakeholders.
- **Log events** (`LogEvents`) – A system-level audit log that records authentication events, configuration changes, and background job execution with timestamps and user attribution.
- **Actuator administration** (`ActuatorAdm`) – Exposes the Spring Boot Actuator health, metrics, and info endpoints through a protected admin UI so operations staff can check server health without shell access.

---

### User & Access Management

- **Self-registration & approval** (`Register`) – New applicants register with their email address and basic profile details. The registration is held in a pending state until a supervisor approves or rejects it, preventing unauthorized access.
- **Role-based menus** – Three distinct navigation shells are rendered based on the authenticated user's role: `UserNotAuthMenu` (public/guest), `UserAuthMenu` (authenticated applicant), and the administrative shell inside `Administrate` (supervisor/regulator). Each role sees only the functions it is authorized to use.
- **Admin password management** (`ChangePassAdmin`) – Administrators can reset any user's password from the admin panel without requiring the user to go through a self-service reset flow.
- **Person management** (`Persons`, `PersonSelector`, `PersonSpecial`) – Structured person records (name, contact details, role) are maintained separately from login accounts, allowing one person to be linked to multiple roles or authorities. A searchable person picker is used across workflows wherever a responsible individual must be named.
- **Regulatory authority management** (`Authorities`, `Authority`) – The organizational directory of national regulatory authorities and their departments is maintained here. Each authority record stores contact information, linked staff members, and the workflows they are responsible for.
- **OAuth2 security** – The server (`pharmadex2`) is secured with Spring Security using both OAuth2 Client (for SSO integration) and OAuth2 Resource Server (for API token validation), in addition to form-based login with Spring Session JDBC for stateful browser sessions.

---

### Import & Legacy Data

- **Application data import — Type A** (`Import_A`) – Bulk import of product applications from a structured Excel template. Designed for initial population of the register when migrating from a spreadsheet-based system.
- **Application data import — Type B** (`Import_B`) – A second import pathway supporting a different source data layout, enabling integration with heterogeneous legacy systems.
- **ATC code import** (`Import_ATC`) – Imports the full or partial WHO ATC classification hierarchy from a standard Excel file, updating existing codes in place and adding new ones.
- **Message import** (`Import_Messages`) – Bulk upload of UI label translations, enabling rapid localization of the interface for a new language without manual entry of each label.
- **Legacy data viewer** (`LegacyData`) – Displays raw legacy records alongside the migrated OpenRIMS data so that regulators can compare and validate the migration output.

---

### Localization & Internationalization

- **Multi-language UI** (`Literals`, `Languages`, `Messages`) – All user-visible text strings in the interface are stored as named literals in the database rather than hard-coded. Administrators manage translations per language through the Messages editor. The `Locales` utility resolves the correct string at render time based on the user's selected language.
- **Jalali (Afghan/Persian) calendar** (`jalali-calendar-master`) – A standalone JavaScript calendar library supports full date entry, display, and arithmetic in the Solar Hijri (Jalali) calendar used in Afghanistan, alongside the Gregorian calendar.
- **Nepali date converter** (`date-convertor`) – A Java utility library converts between the Bikram Sambat (Nepali) calendar and the Gregorian calendar. Used as a server-side dependency to store and display dates correctly for Nepal deployments.
- **Locale-aware date & number formats** (`Formats`) – Date formats, decimal separators, and other locale-sensitive display settings are configured per country without code changes.
- **Calendar date picker** (`CalendarPicker`, `FieldDate`, `ViewEditDate`) – The UI date picker adapts to the active calendar system (Gregorian, Jalali, or Nepali) based on the country configuration.

---

### Integration & Utilities

- **Google Maps address integration** (`GoogleMaps`, `AddressForm`, `ProjectMarker`) – Address fields on any form can be enhanced with a Google Maps picker (`@vis.gl/react-google-maps`). Users search by address or drop a pin on the map; coordinates and formatted address are written back to the form automatically. Map markers can be displayed on project/site overview pages.
- **In-browser PDF viewer** (`ApplicationFiles`, `pdf-viewer-reactjs`) – Uploaded PDF supporting documents are rendered inline in the browser without downloading, keeping the reviewer in the application workflow.
- **File upload & resource management** (`FieldUpload`, `WebResource`, `Resources`, `ResourceFilling`, `ResourcesUsage`) – Any form variable can be configured as a file attachment field. Uploaded files are stored server-side and linked to the application record. The Resources module manages a global library of reference documents (SOPs, guidance notes, templates) that can be attached to workflow stages.
- **Email notifications** – Spring Boot Mail integration sends automated email notifications at configurable workflow transition points (e.g. "your application has been assigned for review", "your application requires corrections").
- **GraphQL API** – A Spring GraphQL endpoint (`spring-boot-starter-graphql`) is available alongside the REST API, enabling structured queries by external data consumers and integration partners.
- **Data sources for external consumers** (`DataSources`) – SQL-backed data source definitions expose curated data sets (e.g. approved product lists) as queryable endpoints for data warehouses or third-party portals.
- **Async background jobs** (`AsyncInform`) – Long-running operations (bulk imports, report generation, DWH refresh) run asynchronously in the background with a progress indicator displayed to the user in real time.
- **Configurable dashboard tiles** (`Tiles`, `Tile`, `TileImage`) – The landing page for each user role is composed of configurable tile widgets, each linking to a specific module or workflow. Tile labels, icons, and target URLs are managed in the admin panel.
- **In-app help & content pages** (`HelpFrame`, `Content`) – Each form and workflow step can have a context-sensitive help page linked to it. Help content is stored as HTML pages managed in the admin interface.

---

## In Progress / Planned Features

- Enhanced **EL (Expression Language) Assistant** for building complex workflow conditions without coding
- Expanded **public-facing portal** for applicants to track their applications
- Improved **test process runner** for end-to-end workflow simulation before go-live
- Additional **reporting templates** and export formats
- Extended **API documentation** and developer guides

---

## Technology Stack

### Backend (Server)
| Layer | Technology |
|---|---|
| Framework | [Spring Boot 2.7.x](https://spring.io/projects/spring-boot) (Java 8) |
| ORM / Data Access | [Spring Data JPA](https://spring.io/projects/spring-data-jpa) + [Hibernate ORM](https://hibernate.org/orm/) |
| Database Driver | [Spring Data JDBC](https://spring.io/projects/spring-data-jdbc) + MySQL Connector/J |
| Security | [Spring Security](https://spring.io/projects/spring-security) + OAuth2 Client & Resource Server |
| Session | Spring Session JDBC |
| Templating | [FreeMarker](https://freemarker.apache.org/) |
| API | REST + [Spring GraphQL](https://spring.graphql.org/) |
| Email | Spring Boot Mail (JavaMail) |
| Build | [Apache Maven](https://maven.apache.org/) |
| Utilities | Apache Commons (BeanUtils, Lang3, Validator, Text), Apache POI (Excel), Apache HttpMime |

### Frontend (Client)
| Layer | Technology |
|---|---|
| Framework | [React 17](https://reactjs.org/) |
| UI Components | [Reactstrap 8](https://reactstrap.github.io/) (Bootstrap 4) |
| Bundler | [Webpack 5](https://webpack.js.org/) |
| Package Manager | [npm](https://www.npmjs.com/) |
| Icons | Font Awesome 4 & 5 |
| Maps | [@vis.gl/react-google-maps](https://visgl.github.io/react-google-maps/) |
| Date Handling | [Moment.js](https://momentjs.com/), React Calendar, React Day Picker |
| PDF | pdf-viewer-reactjs |
| Dev Tool | Microsoft Visual Studio Code |

### Database
| Component | Technology |
|---|---|
| Engine | [MySQL Community Server 8](https://dev.mysql.com/downloads/mysql/) |
| Modelling | [MySQL Workbench](https://www.mysql.com/products/workbench/) |

### Additional Modules
| Module | Description |
|---|---|
| `pdxmodel` | Database model and JPA entity project (Spring Boot, Maven) |
| `date-convertor` | Utility library for Nepali (Bikram Sambat) ↔ Gregorian date conversion |
| `jalali-calendar-master` | Afghan/Persian Jalali calendar library |

---

## Repository Structure

```
OpenRIMS/
├── bin/                    # Binary distribution (Windows & Linux)
├── client/                 # React/JS frontend application
│   └── src/components/     # UI components
├── server/                 # Java backend
│   ├── pdxmodel/           # Database access / JPA entity project
│   └── pharmadex2/         # Main web application project
├── database/               # Database schema and initial data
├── date-convertor/         # Nepali date conversion utility
├── jalali-calendar-master/ # Afghan Jalali calendar library
├── deployment_guide/       # Deployment documentation
├── Releases/               # Regular release notes
└── Logos/                  # Project logos and branding
```

---

## Getting Started

Please refer to the **[OpenRIMS Deployment Guide](deployment_guide/OpenRIMS%20Deployment%20Guide.pdf)** for full installation and configuration instructions.

For the initial database, contact **digital@msh.org** (the database dump exceeds GitHub file size limits).

---

## Contact

For more information, contact **digital@msh.org**

---

## License & Disclaimer

**Copyright Management Sciences for Health.**

The OpenRIMS software, documentation and other products, information, materials and services provided by Management Sciences for Health (MSH or Licensor) are provided **"as is."** Licensor hereby disclaims all warranties, whether express, implied, statutory or other (including all warranties arising from course of dealing, usage or trade practice), and specifically disclaims all implied warranties of merchantability, fitness for a particular purpose, title and non-infringement. Without limiting the foregoing, licensor makes no warranty of any kind that this software or documentation, or any other licensor or third-party goods, services, technologies or materials (including any software or hardware), or any products or results of the use of any of them, will meet the users' or other persons' requirements, operate without interruption, achieve any intended result, be compatible or work with any other goods, services, technologies or materials (including any software, hardware, system or network), or be secure, accurate, complete, free of harmful code or error-free. Licensor is not responsible for further development or any future versions of OpenRIMS.

---

