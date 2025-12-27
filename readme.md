📁 Gen Notes: Operation Potemkin (Demo Artifact)

CLASSIFICATION: DEMO_CONVERSION_PROTOCOL
TARGET FILE: demo.html (Copy of nova.html)
DATA SOURCE: demo_payload.json (The Golden Data)

1. Mission Context

We are deploying a "Red Team" demo artifact. The objective is to transform the live, API-dependent nova.html into a deterministic, offline simulation (demo.html). This allows us to present a high-complexity "Quantum Supremacy" scenario to judges without risking internet latency, API quotas, or authentication blocks.

The Golden Rule: The app must feel alive. Loading bars, "thinking" states, and UI animations (nodeBreathing, UniverseFX) must remain fully intact. The logic is faked, but the experience must be real.

2. The Golden Data Protocol

The application brain will be surgically replaced with a static JSON payload (DEMO_DATA).

The Simulation Flow (The "Happy Path"):

Ingestion: User uploads any PDF (e.g., menu.pdf). The app ignores the content but simulates a 1.5s "Reading" process.

The Switcheroo: The app silently loads DEMO_DATA.pdfText (Quantum Physics paper) instead of the user's file.

Analysis: The app "analyzes" the text by returning DEMO_DATA.topics and DEMO_DATA.mindMapData after a 2s delay (simulated latency).

Synthesis: The Video Studio generates a video by instantly loading DEMO_DATA.videoAssets (images + scripts) while displaying a fake "Rendering" progress bar.

3. Technical Implementation Directives

A. Global Injection (The Implant)

Action: Insert the content of demo_payload.json as a global const DEMO_DATA = { ... } at the top of the script (after imports).

Action: Define const DEMO_MODE = true; to flag the simulation state.

Action: Remove the apiKey variable entirely.

B. The Lobotomy (API Mocking)

All fetch calls to Google Cloud must be replaced with Promise wrappers that return DEMO_DATA subsets. Do not just delete them; replace them with these mock functions:

Function

Behavior & Delay

Return Value

extractTextFromPDF(file)

setTimeout(1500)

DEMO_DATA.pdfText

generateContent(prompt)

setTimeout(2000)

Returns topics, mindMapData, or videoAssets script based on keywords in the prompt.

generateImage(prompt)

setTimeout(1000)

Returns a valid URL from DEMO_DATA.topics[i].schematicUrl or videoAssets.

generateAudio(text)

setTimeout(500)

Returns the specific audioUrl from DEMO_DATA.videoAssets if text matches, or a silent fallback.

C. UX Hardwiring

Workspace Mode: When the user toggles "Workspace Mode", the sidebar document list must automatically populate with 4 dummy file entries (Google_Sycamore_Arch.pdf, Surface_Code_Protocol.pdf, etc.) to simulate a multi-doc environment.

Chat Interface: If the user sends a message, return the pre-canned response from DEMO_DATA.chatMessages (or a generic fallback about "Quantum Coherence") after a 1s delay.

4. Regression Protection (Do Not Break)

Visuals: Do NOT remove UniverseCursorFX, KineticMindMap, or the google-glow CSS animations. The visual polish is the main selling point.

State Management: The App component's state (status, stage, progress) must still transition (idle -> processing -> complete) to trigger the correct UI animations.

Error Handling: Ensure the mock functions never throw errors. The ErrorBoundary should remain but never be triggered.

5. Execution Steps for the Agent

Inject the DEMO_DATA constant (from demo_payload.json).

Refactor the 4 API functions (extract, generate...) to use the mocks.

Update the VideoInterface to load assets from DEMO_DATA instead of calling the generation loop.

Verify that no external calls are made.
