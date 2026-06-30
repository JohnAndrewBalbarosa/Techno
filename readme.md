# To-Do List for Techno (SDG 8 and 12)

## General Preparation
- [ ] Define project goals aligned with SDG 8 (Decent Work and Economic Growth), SDG 10 (Reduced Inequalities), and SDG 11 (Sustainable Cities and Communities).
- [ ] Assemble a team and assign roles (e.g., developer, designer, researcher).
- [ ] Research existing solutions and identify gaps.

## Ideation Phase
- [ ] Brainstorm innovative ideas addressing SDG 8, 10, and 11.
- [ ] Validate ideas with mentors or domain experts.
- [ ] Finalize the project concept and scope.

## Development Phase
- [ ] Set up the development environment.
- [ ] Create a project timeline with milestones.
- [ ] Develop a prototype or MVP (Minimum Viable Product).
- [ ] Test the prototype for functionality and usability.

## Presentation Preparation
- [ ] Prepare a pitch deck highlighting the problem, solution, and impact.
- [ ] Create a demo or walkthrough of the project.
- [ ] Practice the presentation with the team.

## Submission
- [ ] Ensure all deliverables meet the hackathon/ideathon requirements.
- [ ] Submit the project before the deadline.

## Post-Hackathon
- [ ] Gather feedback from judges and participants.
- [ ] Plan next steps for project improvement or implementation.

## Additional Notes

- **Theme Update**: The theme now includes SDG 8 (Decent Work and Economic Growth), SDG 10 (Reduced Inequalities), and SDG 11 (Sustainable Cities and Communities). Feel free to interpret these as you see fit, as long as you can explain the reasoning behind your approach.
- **Support Availability**: A "ghost member" will be available to assist all groups with technical challenges, brainstorming, or organizational help. Don’t hesitate to reach out for guidance.
- **Focus on Growth**: The primary goal is personal and team growth. Use this opportunity to practice teamwork, leadership, and presentation skills. Perfection is not required—showing up and learning is what matters.
- **Presentation Day**: Scheduled for May 17. Each group will present one working product, which can be a skeleton, tech demo, or prototype. It doesn’t need to be complete but should demonstrate effort and direction.
- **Group Adjustments**: If you need to change group members or add new ones, please communicate this promptly.
- **Concerns**: For any issues, including the possibility of backing out, reach out for support. The aim is to help everyone grow through this experience.


## Web App To-Do List: Hub and Spoke System for Farmers and City Hall

### Planning Phase
- [ ] Define the project scope and objectives.
- [ ] Identify stakeholders (City Hall, Barangays, Farmers, Merchants).
- [ ] Research existing solutions for crop disaster warnings and SIM-based messaging.
- [ ] Design the hub-and-spoke architecture for the database and communication system.

### Database Design
- [ ] Create a central repository for City Hall.
- [ ] Design data marts for each Barangay to store farmer information.
- [ ] Define database schemas for:
    - Farmer details (name, contact number, crop details).
    - Crop disaster warnings.
    - Transaction logs (buy/sell agreements).
    - Merchant requests and statuses.

### Backend Development
- [ ] Set up the central database and Barangay data marts.
- [ ] Implement APIs for:
    - Sending crop disaster warnings.
    - Receiving and processing farmer responses.
    - Handling merchant requests.
- [ ] Develop AI integration for analyzing farmer responses and generating actionable insights.
- [ ] Implement JSON-based messaging for communication between Barangays and City Hall.

### Frontend Development
- [ ] Design a user-friendly interface for City Hall to manage repositories and monitor transactions.
- [ ] Create a dashboard for Barangays to manage farmer data and send/receive messages.
- [ ] Develop a portal for merchants to submit requests and track statuses.

### SIM Messaging Integration
- [ ] Research and integrate a broadband-to-SIM messaging service.
- [ ] Implement functionality to:
    - Send disaster warnings to farmers.
    - Receive farmer responses (e.g., "YES" and price).
    - Forward responses to the central repository.

### Features Development
- [ ] Implement disaster warning prompts for farmers.
- [ ] Add functionality for farmers to agree to sell crops at a specific price.
- [ ] Abstract farmer details for merchants while showing transaction statuses.
- [ ] Add job posting features for City Hall and Barangays.

### Testing and Deployment
- [ ] Test the system for functionality, scalability, and usability.
- [ ] Conduct pilot testing in a few Barangays.
- [ ] Deploy the system city-wide and provide training for City Hall and Barangay IT teams.

### Post-Deployment
- [ ] Monitor system performance and gather user feedback.
- [ ] Plan for scalability by adding more Barangays to the hub-and-spoke system.
- [ ] Continuously improve features based on feedback and emerging needs.

## Architecture (UML)

```mermaid
graph TD
    CityHall["🏛️ City Hall<br/>(Central Hub)"]
    Barangay["📍 Barangay<br/>(Data Mart)"]
    Farmers["👨‍🌾 Farmers<br/>(SMS Access)"]
    Merchants["🏪 Merchants<br/>(Web Portal)"]
    
    subgraph "Backend (Python Flask)"
        DB["🗄️ Central Database<br/>(Hub)"]
        DataMart["📊 Barangay Data Mart<br/>(Spoke)"]
        APIs["🔌 APIs<br/>(Farmers, Orders,<br/>Products, Users,<br/>Government)"]
        AIMod["🤖 AI Module<br/>(Disaster Analysis)"]
    end
    
    subgraph "Communication Layer"
        SIMGateway["📱 SIM/SMS Gateway<br/>(Broadband-to-SIM)"]
        JSONMessaging["📦 JSON Messaging<br/>(Barangay ↔ Hub)"]
    end
    
    CityHall -->|Manage Warnings| APIs
    Barangay -->|Forward Messages| JSONMessaging
    JSONMessaging -->|Update| DataMart
    DataMart -->|Sync| DB
    
    Farmers -->|SMS Response<br/>YES + Price| SIMGateway
    SIMGateway -->|Parse| APIs
    APIs -->|Analyze| AIMod
    AIMod -->|Insights| CityHall
    
    Merchants -->|Submit Requests| APIs
    APIs -->|Track Status| Merchants
    
    APIs -->|Send Warnings| SIMGateway
    SIMGateway -->|Alert| Farmers
```