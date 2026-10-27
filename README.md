# ScamShield AI
## Educational scam-awareness chatbot for India

**Student:** Imrul Kayes Shaikh  
**Registration number:** 1000700  
**Assessment:** Creating Intelligent Chatbots for Practical Applications — SA-1  
**Course:** Artificial Intelligence: Real-World Applications and Implications

## Live chatbot

[Open ScamShield AI on Vercel](https://idai101-1000700-imrul-kayes-shaikh.vercel.app/)

Open the chat bubble and type **Hi**. Use fictional examples or a redacted summary only.

## Project overview and user needs

ScamShield AI helps people pause when they receive suspicious requests, recognise warning signs and consider appropriate next steps. The intended audience includes students, families and people unfamiliar with common online scams in India.

The project addresses three anticipated needs: simple explanations, a guided way to describe a suspicious request, and clear limits on what a chatbot can establish. These are design assumptions based on the scenario, not findings from completed user interviews or surveys.

The assistant covers job offers, UPI requests, phishing, requests for secret codes, impersonation and remote-access concerns. It also offers a short safety quiz. It is an educational prototype: it does not inspect accounts, authenticate senders, scan links, establish whether a message is fraudulent, recover money or submit reports.

## Implementation and integration

The interface is a responsive HTML, CSS and JavaScript page. Google Dialogflow Messenger connects visitors to the Dialogflow ES agent. Dialogflow performs intent matching, entity extraction and context handling; the page displays the embedded conversation.

- Agent display name: `ScamShield_AI`
- Agent ID in the embed: `34e17922-5acf-44a2-8b67-5af63e9e7f46`
- Language: English
- Website hosting: Vercel
- Source control: GitHub
- No custom webhook, Python backend, GPT integration or developer-supplied API key is used by this website. The Google-hosted Messenger integration communicates with Dialogflow.
- Prompt buttons on the webpage copy suggested text; visitors paste it into the chat. They do not automatically submit messages.

## Intent design

The prepared agent export contains **36 intents**, including **5 fallback intents**, and **12 custom entities**. Its 31 non-fallback intents contain 12 example training phrases each (372 total). These are export configuration counts, not an accuracy score or a fresh audit of the live console.

| Intent(s) | Purpose |
| --- | --- |
| Welcome | Introduces the assistant, scope and privacy boundaries. |
| MainMenu | Presents the main conversation choices. |
| AboutLimits | Explains what the assistant can and cannot establish. |
| Privacy | Explains safe use without entering private details. |
| GuidedCheck | Collects topic, contact channel and requested action, then summarises them. |
| ExplainCheck | Uses the review context to explain caution about the described request. |
| NoExposure | Handles the visitor reporting that nothing was shared. |
| SafeVerification | Explains independent verification. |
| SafetyTips | Provides general scam-awareness guidance. |
| FakeJobAdvice | Handles suspicious job-offer questions. |
| UPIReceiveSafety | Handles questions about receiving UPI payments. |
| QRSafety | Handles QR-code concerns. |
| OTPAdvice | Handles requests for secret codes. |
| PhishingAdvice | Handles suspicious links and messages. |
| ImpersonationAdvice | Handles claimed identities and impersonation concerns. |
| PressureAdvice | Explains urgency, threats and other pressure tactics. |
| MoneyLostEmergency | Routes reported financial-loss situations to urgent guidance. |
| SecretSharedEmergency | Handles reports of disclosed secrets. |
| ClickedLink | Handles reports of opening a suspicious link. |
| RemoteAccessEmergency | Handles remote-access concerns. |
| ReportingSteps | Explains reporting routes. |
| EvidenceChecklist | Describes evidence categories to preserve outside the chatbot. |
| HumanHelp | Directs visitors toward human assistance. |
| CancelAndRestart | Provides an exit or restart route. |
| QuizStart | Starts the three-question safety quiz. |
| Quiz1Safe, Quiz1Unsafe | Provide feedback for the first question. |
| Quiz2Safe, Quiz2Unsafe | Provide feedback for the second question. |
| Quiz3Safe, Quiz3Unsafe | Provide feedback for the final question. |
| DefaultFallback | Handles unmatched general input. |
| ReviewFallback | Handles unmatched input while reviewing a request. |
| Quiz1Fallback, Quiz2Fallback, Quiz3Fallback | Keep unmatched quiz input within the relevant question. |

## Entities and parameters

Entities capture categories, not actual passwords, payment credentials or personal documents.

| Entity | Information represented | Example |
| --- | --- | --- |
| scam_type | Topic of the request | job offer |
| contact_channel | Where the contact arrived | WhatsApp |
| requested_action | What the sender requested | send money |
| claimed_identity | Identity claimed by the sender | recruiter |
| sensitive_item | Type of secret involved | OTP |
| payment_method | Payment category | UPI |
| link_type | Link or QR category | shortened link |
| pressure_tactic | Pressure used in the request | urgent deadline |
| job_offer_type | Job category | internship |
| report_need | Reporting situation | suspicious contact |
| evidence_type | Evidence category | screenshots |
| quiz_choice | Recognised quiz answer | keep the code private |

### Slot filling and contexts

`GuidedCheck` requires three parameters: `scam_type`, `contact_channel` and `requested_action`. If information is missing, the agent asks for it before returning a summary.

Example flow: **check a message → job offer → WhatsApp → send money**.

The `review` context supports “Why be cautious” after that summary. The `quiz1`, `quiz2` and `quiz3` contexts separate quiz stages. Context-specific fallback intents are configured for review and each quiz stage. Messenger rich responses provide interactive options where supported.

## Repository contents

| File | Purpose |
| --- | --- |
| index.html | Complete website, styling, prompt-copy behaviour and Dialogflow Messenger embed. |
| README.md | Project overview, agent design, hosting instructions and evidence status. |
| deliverables/ScamShield_AI_ES_Import.zip | Importable Dialogflow ES agent backup. |
| deliverables/Imrul_Kayes_Shaikh_1000700_ScamShield_SA1.pdf | Final three-page submission summary. |

The intent and entity inventory above was checked against the included prepared Dialogflow ES export.

## Deployment instructions

1. Import this GitHub repository into Vercel.
2. Select **Other** as the application preset and keep the root directory as `./`.
3. Leave build, output and install command overrides disabled for this buildless page.
4. Use a lowercase Vercel project name and deploy.
5. Open the production domain and use the chat bubble.
6. For a different agent, enable its Dialogflow ES Messenger integration and replace the embed attributes with the snippet supplied by that agent.

No environment variables or secret files are needed for this implementation. The agent must remain available through its Messenger integration. Opening the HTML through `file://` is not equivalent to using the hosted website.

## Demonstrated results and limitations

| Check | Evidence available | Status |
| --- | --- | --- |
| Vercel website deployment | Student-shared Vercel screenshot showing Ready and the deployed page | Demonstrated |
| Live greeting | Student-shared Vercel screenshot showing “Hi” and the ScamShield introduction | Demonstrated |
| Guided request collection | Earlier pasted Dialogflow responses for job offer, WhatsApp and send money, including the correct summary | Demonstrated through reported console interaction |
| Contextual explanation | Earlier pasted “Why be cautious” response retained those details | Demonstrated through reported console interaction |
| Nothing shared response | Earlier pasted response addressed no reported exposure | Demonstrated through reported console interaction |
| Five separate realistic end-to-end scenarios | No complete evidence set recorded here | Not completed |
| Complete quiz, fallback and emergency branches on Vercel | No completed evidence recorded here | Not verified |

The guided conversation and its follow-ups are one workflow, not five separate scenarios. Further testing was deferred at the student's request. No overall accuracy percentage, full test-suite pass or guaranteed assessment result is claimed.

### Recorded deployment issue and improvement

Earlier local-file and hosted attempts displayed the widget but did not return replies; a local-file screenshot showed a CORS error. A later student screenshot on Vercel showed a successful greeting. This demonstrates a working interaction on Vercel at that time, but does not establish the root cause of the earlier failures or validate every conversation branch.

## Privacy, safety and responsible use

Use made-up examples. Do not enter real OTPs, PINs, passwords, card details or identity documents. The assistant cannot prove a sender is genuine or a request is safe. It should complement independent checks and appropriate human support.

The page does not implement its own chat database. Messages are processed through Google's Messenger integration; hosting and service providers may maintain operational logs. This project does not promise zero retention.

## References and assistance

- The supplied SA-1 assessment brief and rubric define the project requirements.
- The implementation uses Google Dialogflow ES and its Dialogflow Messenger embed.
- ChatGPT assisted with preparing the agent configuration, website and documentation. Student-shared screenshots and pasted replies are identified above; unperformed tests are not presented as completed.

## Submission status

The website is deployed and a live greeting has been demonstrated. The detailed README, Dialogflow ES backup and final submission PDF are included. Access has been invited for the assessor account and is pending acceptance. The outstanding limitation is the incomplete five-scenario testing evidence described above.
