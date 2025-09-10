### AyurSutra Clinic Flowchart

```mermaid
graph TD
    classDef shaded fill:#f0f0f0,stroke:#333,stroke-width:2px

    subgraph Patient Flow
        Patient --> LoginAsPatient[Login as Patient]
        LoginAsPatient --> BookAppointment[Book Appointment <br/> <small>Check availability</small>]
        BookAppointment --> Payment
        Payment --> Confirmation
        Confirmation --> TrackProgress
    end

    subgraph Clinic Staff Portal
        ClinicStaff[Clinic Staff] --> UserLogin[User Login Portal]
        UserLogin --> AdminBox{Admin}
        
        subgraph A
            AdminBox -- Reception --> LoginAdmin[Login as Reception]
            LoginAdmin --> ManageSchedule[Manage Schedule <br/> <small>Add/Editing Appointments for all staff</small>]

            AdminBox -- Doctor --> ManagePatientRecords[Manage Patient Records]
            ManagePatientRecords --> UpdatePatientRecords[Update Records, prescriptions]

           
        end
    end

    subgraph Management Portal
        Management --> AnalyticsDashboard["View Analytics Dashboard <br/> ☐ Core Metrics <br/> ☐ Appointment booking <br/> ☐ Revenue"]
       
        %% --- NEW FLOW ---
       Management --> ViewStaffPerformance["View Staff Performance <br/><small>Client Engagement</small>"]

    end

    subgraph Database
        CentralDB[(Central Patient Database)]
    end

    %% --- Connections ---
    Confirmation --> ManageSchedule
    ManageSchedule --> CentralDB
    UpdatePatientRecords --> CentralDB
   
    CentralDB --> AnalyticsDashboard
    CentralDB --> ViewStaffPerformance

   
