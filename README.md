# Holmes: A Text-Based Crime Investigation Game Powered by an LLM

Holmes is an interactive, text-based crime investigation game powered by a large language model (LLM). With each replay, the game offers a fresh narrative, ensuring a unique experience for players every time.

## About

Holmes challenges players to solve a murder mystery by interrogating a set of suspects. The game's story is dynamically generated by an LLM, creating a new murder plot, timeline of events, and detailed descriptions of suspects with each replay. Players interact with the game's characters (suspects) through Langchain agents, allowing for immersive interrogation sessions.

## Features

- **Dynamic Story Generation**: Utilizing LLM's capabilities, Holmes creates a unique murder mystery narrative each time it's played.
- **Interrogate Suspects**: Players can question Langchain agents representing each suspect to uncover clues and make educated guesses about the murderer.
- **Retrieval Augmented Generation (RAG)**: Suspects' memories are stored in ChromaDB, enhancing the interrogation experience.

## How It Works

### Flow for Story Generation:

1. **Initial Setup**: The LLM acts as a murder mystery novelist and fills out a series of JSON schemas detailing the murder, the victim, and the four suspects. It is specified that the murder must have occurred at an event at which all four suspects and the victim were present.
2. **Building the Timeline**: 
   - Generate a timeline with ten timestamps at 15-minute intervals.
   - Designate interactions between suspects at specific timestamps.
   - Detail each suspect's actions at every timestamp.
   - Simulate shared interactions based on the timeline.
3. **Creating Suspect Agents**:
   - Generate a memory stream for each suspect, detailing their experiences throughout the events.
   - Create a `SuspectAgent` object for each suspect. Their memory streams are chunked, embedded, and stored in a ChromaDB instance.
4. **Interrogation**:
   - Players can question each suspect. The nature of the prompts varies based on the suspect's innocence or guilt.
   - The game concludes once the player decides on the guilty suspect.

### Challenges & Implementation Details:

- **Working with an LLM**: Utilizing GPT’s function calling feature required extensive parsing to fill out the JSON schemas. However, ensuring the returned JSON string's validity posed a challenge, especially during timeline generation. To resolve this, the LLM was leveraged to correct any JSON syntax errors.
- **Data Storage**: A hierarchy of objects (`Timestamp`, `SuspectAgent`, etc.) was devised to hold the generated text. The `Plot` object encapsulates all game information, allowing easy data serialization.
- **Flexibility**: Currently, Holmes uses OpenAI’s `gpt-3.5-turbo-16k` for its LLM. However, by replacing OpenAI calls with Langchain chains/agents, almost any LLM could be integrated into the game.

## Future Plans

- **Integrate Multiple LLMs**: Plan to support different LLMs by replacing OpenAI calls with Langchain chains/agents.
- **Enhance Game Mechanics**: Look forward to deepening the game mechanics for a richer player experience.

## Author

[Your Name] - Sophomore at [Your College Name]. Seeking internship opportunities.
