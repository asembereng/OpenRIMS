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
- **Application lifecycle management** – Create, submit, track, amend, renew, and de-register medicine/product applications
- **Activity manager** – Assign, manage, and track activities within a workflow for each application
- **Inspection management** – Schedule and manage inspection workflows
- **Amendment workflows** – Support for amending existing approved registrations
- **Renewal workflows** – Track and process registration renewal applications
- **De-registration workflows** – Manage the withdrawal of registered products
- **Public permit data** – Expose approved permit information to public users

### Workflow & Process Configuration
- **Configurable workflows** – Define and customize multi-step approval processes without coding via the Process Configurator
- **Workflow validation** – Built-in process validator to check workflow integrity
- **Activity history & timelines** – Full audit trail of all actions taken on an application
- **To-do lists** – User-facing task queues for pending activities
- **Scheduler / host schedule** – Background job scheduling for automated tasks
- **Re-assignment of activities and users** – Reassign tasks across team members

### Data & Dictionary Configuration
- **Data configurator** – Dynamically define and customize data structures and form layouts for any application type
- **Dictionary management** – Hierarchical dictionary/code-list editor with multi-level support
- **ATC codes** – Manage the WHO Anatomical Therapeutic Chemical classification codes
- **INN (International Non-proprietary Names)** – Manage INN data for medicines
- **Excipients** – Manage excipient reference data

### Monitoring & Reporting
- **Monitoring dashboard** – Real-time, scheduled, and full-search monitoring views
- **External reports** – Generate and export configurable reports
- **Log events viewer** – System-level event log for auditing
- **Actuator administration** – Health and metrics monitoring via Spring Boot Actuator

### User & Access Management
- **User registration & authentication** – User self-registration with admin approval; password management
- **Role-based access control** – Differentiated menus and functions for authorized, guest, and admin users
- **OAuth2 / security integration** – Secured with Spring Security and OAuth2
- **Person management** – Manage person records linked to user accounts
- **Authorities administration** – Manage regulatory authority entities and their staff

### Import & Legacy Data
- **Data import (A/B)** – Bulk import of application and product data
- **ATC code import** – Import WHO ATC classification data
- **Workflow import** – Import preconfigured workflow definitions
- **Legacy data migration** – Support for migrating data from previous system versions

### Localization & Internationalization
- **Multi-language support** – Configurable UI literals and messages for any language
- **Jalali (Afghan/Persian) calendar** – Full support for the Afghan solar calendar
- **Nepali date converter** – Utility for converting Nepali (Bikram Sambat) dates
- **Locale-aware formats** – Configurable date and number formats per country

### Integration & Utilities
- **Google Maps integration** – Location/address fields with Google Maps support
- **PDF viewer** – In-browser PDF document viewing
- **Email notifications** – Integrated mail service for workflow notifications
- **GraphQL API** – Internal GraphQL endpoint alongside the REST API
- **Web resources management** – Upload and manage reference documents and resources
- **Help / content pages** – Configurable in-app help and informational pages

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

