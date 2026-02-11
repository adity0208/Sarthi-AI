# Requirements Document

## Introduction

Sarthi-AI is a voice-first, multilingual medical triage system designed for rural India. The system helps users distinguish between minor symptoms and life-threatening emergencies through a 4-agent orchestration workflow, providing culturally sensitive medical guidance to non-tech-savvy users with limited digital literacy.

## Glossary

- **Sarthi_System**: The complete voice-first medical triage application
- **Safety_Agent**: Priority 1 agent that scans for emergency keywords and overrides all other logic
- **Entity_Extractor**: Agent that transcribes voice input and identifies medical entities
- **RAG_Agent**: Retrieval-Augmented Generation agent that queries clinical databases
- **Empathy_Agent**: Agent that ensures culturally sensitive and calm response delivery
- **Red_Flag_Keywords**: Predefined emergency medical terms that trigger immediate emergency response
- **Physician_Deliverable**: Structured H&P (History & Physical) summary for healthcare workers
- **Voice_Loop**: Complete cycle from user voice input to system voice response
- **ASHA_Worker**: Accredited Social Health Activist - community health worker in rural India
- **H_and_P_Note**: History and Physical examination note format used by physicians

## Requirements

### Requirement 1: Emergency Detection and Override

**User Story:** As a rural citizen experiencing a medical emergency, I want the system to immediately recognize life-threatening symptoms, so that I receive urgent care instructions without delay.

#### Acceptance Criteria

1. WHEN the Safety_Agent detects Red_Flag_Keywords in user input, THE Sarthi_System SHALL immediately provide emergency contact information and hospital directions
2. WHEN Red_Flag_Keywords are detected, THE Safety_Agent SHALL override all other agent processing and bypass normal triage workflow
3. WHEN emergency instructions are provided, THE Sarthi_System SHALL log the interaction with timestamp and user location for audit purposes
4. THE Safety_Agent SHALL maintain a comprehensive database of Red_Flag_Keywords in Hindi and English covering cardiac, respiratory, neurological, and trauma emergencies
5. WHEN multiple agents are processing simultaneously, THE Safety_Agent SHALL have absolute priority and terminate other agent operations upon Red_Flag_Keyword detection

### Requirement 2: Multilingual Voice Processing

**User Story:** As a rural user who primarily speaks Hindi, I want to communicate with the system in my preferred language, so that I can accurately describe my symptoms without language barriers.

#### Acceptance Criteria

1. WHEN a user speaks in Hindi or English, THE Entity_Extractor SHALL transcribe the audio with 95% accuracy or higher
2. WHEN transcription is complete, THE Entity_Extractor SHALL identify medical symptoms, duration, and severity from the transcribed text
3. WHEN voice input is received, THE Sarthi_System SHALL process and respond within 2 seconds to maintain conversational flow
4. THE Sarthi_System SHALL support voice input and output in both Hindi and English with appropriate regional accents
5. WHEN transcription confidence is below 80%, THE Sarthi_System SHALL request clarification from the user

### Requirement 3: Clinical Knowledge Retrieval

**User Story:** As a user seeking medical guidance, I want the system to provide accurate medical information based on verified clinical sources, so that I receive reliable health advice.

#### Acceptance Criteria

1. WHEN symptoms are identified, THE RAG_Agent SHALL query verified clinical databases through Amazon Bedrock Knowledge Bases
2. WHEN clinical information is retrieved, THE RAG_Agent SHALL provide evidence-based triage recommendations appropriate for the symptom severity
3. THE RAG_Agent SHALL maintain access to clinical databases covering common conditions prevalent in rural India
4. WHEN no relevant clinical information is found, THE RAG_Agent SHALL recommend consulting a healthcare professional
5. THE RAG_Agent SHALL NOT provide prescription recommendations for Schedule H controlled substances

### Requirement 4: Cultural Sensitivity and Communication

**User Story:** As a rural user from a traditional background, I want the system to communicate in a respectful and culturally appropriate manner, so that I feel comfortable sharing sensitive health information.

#### Acceptance Criteria

1. WHEN providing medical advice, THE Empathy_Agent SHALL use calm, non-alarmist language appropriate for rural Indian cultural context
2. WHEN sensitive topics are discussed, THE Empathy_Agent SHALL maintain respectful tone while ensuring medical accuracy
3. THE Empathy_Agent SHALL avoid medical jargon and use simple, understandable language in the user's preferred language
4. WHEN delivering potentially concerning information, THE Empathy_Agent SHALL balance honesty with emotional support
5. THE Empathy_Agent SHALL incorporate culturally appropriate greetings and communication patterns

### Requirement 5: Healthcare Worker Integration

**User Story:** As an ASHA worker, I want to receive structured medical summaries from user interactions, so that I can provide informed follow-up care and communicate effectively with physicians.

#### Acceptance Criteria

1. WHEN a triage session is complete, THE Sarthi_System SHALL generate a Physician_Deliverable summary in H_and_P_Note format
2. WHEN generating summaries, THE Sarthi_System SHALL include patient symptoms, duration, severity assessment, and recommended actions
3. THE Physician_Deliverable SHALL be formatted according to standard medical documentation practices
4. WHEN ASHA_Workers access summaries, THE Sarthi_System SHALL provide them in both Hindi and English
5. THE Sarthi_System SHALL maintain patient privacy while providing necessary clinical information to authorized healthcare workers

### Requirement 6: System Performance and Reliability

**User Story:** As a rural user with limited internet connectivity, I want the system to work reliably on slow networks, so that I can access medical guidance when needed.

#### Acceptance Criteria

1. WHEN operating on 3G/4G networks with limited bandwidth, THE Sarthi_System SHALL maintain functionality with optimized data usage
2. WHEN processing Voice_Loops, THE Sarthi_System SHALL complete the full cycle within 2 seconds under normal network conditions
3. WHEN network connectivity is poor, THE Sarthi_System SHALL provide graceful degradation with offline emergency contact information
4. THE Sarthi_System SHALL achieve 99% accuracy in emergency detection across all supported languages
5. WHEN system errors occur, THE Sarthi_System SHALL log errors and provide user-friendly error messages

### Requirement 7: Data Security and Audit

**User Story:** As a healthcare system stakeholder, I want all medical interactions to be securely logged and auditable, so that we can ensure compliance and improve system performance.

#### Acceptance Criteria

1. WHEN user interactions occur, THE Sarthi_System SHALL encrypt and store all session data in compliance with healthcare privacy regulations
2. WHEN storing audit logs, THE Sarthi_System SHALL include timestamps, user location, symptoms discussed, and recommendations provided
3. THE Sarthi_System SHALL maintain encrypted storage of all voice recordings and transcriptions for quality assurance
4. WHEN accessing stored data, THE Sarthi_System SHALL require appropriate authentication and authorization
5. THE Sarthi_System SHALL automatically purge personal health information according to data retention policies

### Requirement 8: User Interface and Accessibility

**User Story:** As a non-tech-savvy rural user, I want a simple interface that I can easily understand and use, so that I can access medical guidance without technical difficulties.

#### Acceptance Criteria

1. WHEN users access the system, THE Sarthi_System SHALL provide a mobile-responsive interface with prominent "Press to Speak" functionality
2. WHEN displaying information, THE Sarthi_System SHALL use large, clear text and intuitive icons suitable for users with limited digital literacy
3. THE Sarthi_System SHALL provide visual feedback during voice processing to indicate system status
4. WHEN voice input is not available, THE Sarthi_System SHALL provide alternative text input methods
5. THE Sarthi_System SHALL support accessibility features for users with hearing or vision impairments