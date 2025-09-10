### AyurSutra Clinic Flowchart

```mermaid
%%{init: {"theme":"default","themeVariables": {
  "clusterBkg": "#f9f9f9",
  "clusterBorder": "#444",
  "clusterTextColor": "#000"
}}}%%

graph TD
    %% --- Theme & Styles ---
    classDef shaded fill:#f9f9f9,stroke:#444,stroke-width:2px,rx:10,ry:10,color:#000,font-weight:bold
    classDef database fill:#e8f4ff,stroke:#0077b6,stroke-width:2px,rx:10,ry:10,color:#000,font-weight:bold
    classDef decision fill:#f2f2f2,stroke:#888,stroke-width:2px,rx:10,ry:10,color:#000,font-weight:bold
    classDef process fill:#e6ffe6,stroke:#388e3c,stroke-width:2px,rx:10,ry:10,color:#000,font-weight:bold

    %% --- Patient Flow ---
    subgraph Patient_Flow [👩‍⚕️ Patient Flow]
        Patient([Patient]):::shaded --> LoginAsPatient[Login as Patient]:::process
        LoginAsPatient --> BookAppointment[Book Appointment <br/> <small>Check availability</small>]:::process
        BookAppointment --> Payment[Make Payment]:::process
        Payment --> Confirmation[Get Confirmation]:::process
        Confirmation --> TrackProgress[Track Progress]:::process
    end

    %% --- Clinic Staff Portal ---
    subgraph Clinic_Staff [🏥 Clinic Staff Portal]
        ClinicStaff([Clinic Staff]):::shaded --> UserLogin[User Login Portal]:::process
        UserLogin --> AdminBox{Admin Roles}:::decision

        subgraph Admin_Area [⚙️ Admin Area]
            AdminBox -- Reception --> LoginAdmin[Login as Reception]:::process
            LoginAdmin --> ManageSchedule[Manage Schedule <br/> <small>Add/Edit Appointments</small>]:::process

            AdminBox -- Doctor --> ManagePatientRecords[Manage Patient Records]:::process
            ManagePatientRecords --> UpdatePatientRecords[Update Records & Prescriptions]:::process
        end
    end

    %% --- Management Portal ---
    subgraph Management_Portal [📊 Management Portal]
        Management([Management]):::shaded --> AnalyticsDashboard["View Analytics Dashboard <br/> ☐ Core Metrics <br/> ☐ Appointment Booking <br/> ☐ Revenue"]:::process
        Management --> ViewStaffPerformance["View Staff Performance <br/><small>Client Engagement</small>"]:::process
    end

    %% --- Central Database ---
    subgraph Database [💾 Central Database]
        CentralDB[(Central Patient Database)]:::database
    end

    %% --- Connections ---
    Confirmation --> ManageSchedule
    ManageSchedule --> CentralDB
    UpdatePatientRecords --> CentralDB
   
    CentralDB --> AnalyticsDashboard
    CentralDB --> ViewStaffPerformance

