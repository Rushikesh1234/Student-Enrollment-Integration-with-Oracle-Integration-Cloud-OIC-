# Student Enrollment Integration with Oracle Integration Cloud (OIC)

I built this project to demonstrate a **real-world integration scenario** where student enrollment data from a portal is automatically synchronized with Oracle Fusion Cloud using Oracle Integration Cloud (OIC). The goal is for me to learn OIC fundamentals, integration patterns, data transformation, error handling, and monitoring in a practical way.

---

## **Problem I’m Solving**
At universities, student registrations often happen in a separate portal system, but official records live in Oracle Fusion. Manual entry can lead to:

- Duplicate student records  
- Data entry errors  
- Delayed registration processing  
- Lack of real-time visibility

I wanted to solve this problem using middleware so everything happens automatically and in real-time.

---

## **My Solution**
I use **OIC as a middleware integration** that:

- Receives student registration data from a portal (Google Forms / Apps Script)  
- Validates and transforms the data  
- Calls Oracle Fusion Cloud API to create official student records  
- Returns success/failure messages to the portal  
- Provides monitoring, logging, and error handling  

---

## **Actors / Systems**

| Actor/System | Role |
|--------------|------|
| Student | Submits registration in the portal |
| Student Portal | My non-Fusion system; triggers API call to OIC |
| OIC | Middleware; validates data, transforms it, calls Fusion API |
| Oracle Fusion Cloud | Maintains official student records |
| Admin / Monitoring Team | Tracks integration, handles errors |

---

## **Tools / Components I Used**
- **Google Forms + Apps Script**: Student portal and API trigger  
- **Oracle Integration Cloud (OIC)**:
  - REST Adapter (Inbound)  
  - Oracle Fusion Adapter (Outbound)  
  - Data Mapper / Transformation  
  - Fault Handling / Notifications  
- **Oracle Fusion Cloud**: Student record management

---

## **System Workflow**

```
[Student fills Google Form]
          ↓
[Google Apps Script triggers POST to OIC REST API]
          ↓
[OIC Integration Flow]
   - Receive JSON payload
   - Validate fields (mandatory, format)
   - Transform data to Fusion API format
   - Call Fusion Student API (Create Student)
   - Handle errors (duplicates, missing info)
          ↓
[Return Success/Failure to Google Form / Apps Script]
          ↓
[Admin Dashboard / Monitoring in OIC]
```

---

## **Step-by-Step OIC Implementation**
- An inbound REST API is created in OIC to receive student registration data.  
- JSON payload with fields such as Name, DOB, Email, Course, Phone, and Address is received.  
- Mandatory fields are validated and email format is checked.  
- Student portal JSON fields are mapped to Fusion API structure.  
- Errors are handled:
  - Duplicate email → `"Student with this email already exists."`  
  - Missing fields → `"Missing required field: <field>"`  
- Oracle Fusion Student Cloud API is called to create student records.  
- Real-time and batch integration processes are implemented.  
- Conditional routing and orchestration are added (e.g., undergrad vs grad students, approval flows).  
- Logging and monitoring are set up in the OIC dashboard.  
- Email notifications are sent for failures.  
- Endpoints are secured with OAuth / API Key.

---

## **Future Enhancements**
- Integrate additional student data sources (Excel, other portals)  
- Add advanced orchestration with approvals and notifications  
- Build an analytics dashboard for enrollment trends


