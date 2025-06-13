# Riyad's VibeBot

## Overview
Riyad's VibeBot is an interactive chatbot that leverages the power of Large Language Models (specifically a DeepSeek model via OpenRouter.ai) to provide dynamic and engaging conversations. It features a Node.js backend to securely manage the API key and a frontend interface built with React and Tailwind CSS. The bot also includes a fallback mechanism to predefined responses for certain queries.

## Features
*   Interactive chat interface.
*   Powered by a Large Language Model (DeepSeek via OpenRouter) for dynamic responses.
*   Secure API key handling using a Node.js backend server.
*   Fallback to predefined, manually crafted responses for specific queries and topics.
*   Visually appealing interface with a Three.js animated background.

## Setup Instructions

### Prerequisites
*   Node.js and npm (Node Package Manager) installed on your system. You can download them from [nodejs.org](https://nodejs.org/).
*   An API key from [OpenRouter.ai](https://openrouter.ai/). Sign up and obtain your key.

### Backend Setup
1.  **Clone the Repository / Download Files:**
    If this project is in a Git repository, clone it:
    ```bash
    git clone <repository_url>
    cd <repository_directory>
    ```
    Otherwise, download all project files (`index.html`, `server.js`, `package.json`, etc.) into a single project directory.

2.  **Navigate to Project Directory:**
    Open your terminal or command prompt and navigate to the root directory of the project.

3.  **Create `.env` File:**
    In the root of the project directory, create a new file named `.env`.

4.  **Add API Key to `.env` File:**
    Open the `.env` file and add your OpenRouter API key in the following format:
    ```
OPENROUTER_API_KEY=your_actual_api_key_here
    ```
    Replace `your_actual_api_key_here` with the API key you obtained from OpenRouter.ai.

5.  **Install Backend Dependencies:**
    In your terminal, run the following command to install the necessary Node.js packages (Express.js and Axios):
    ```bash
    npm install
    ```

6.  **Start the Backend Server:**
    Run the following command to start the Node.js server:
    ```bash
    node server.js
    ```
    By default, the server will start and listen on `http://localhost:3000`. You should see a message in the console like: `Server listening at http://localhost:3000`.

### Frontend Usage
1.  **Open `index.html`:**
    Once the backend server is running, open the `index.html` file directly in your web browser.
    *   You can typically do this by double-clicking the file or right-clicking and choosing "Open with" your preferred browser.

2.  **Start Chatting:**
    The chat interface will load, and you can start interacting with Riyad's VibeBot!

## How it Works
1.  **Frontend Interaction:** The user types a message in the chat interface (`index.html`).
2.  **Fallback Check:** The frontend JavaScript first checks if the message matches any predefined queries for a manual, hardcoded response.
3.  **API Call (if needed):**
    *   If the message triggers a specific manual response, that response is displayed.
    *   If the message results in a default manual response (indicating no specific match), the frontend makes a `fetch` request to the `/api/chat` endpoint on the backend Node.js server.
4.  **Backend Processing:** The Node.js server (`server.js`) receives the request.
    *   It retrieves the `OPENROUTER_API_KEY` securely from the `.env` file (which is not accessible to the client).
    *   It makes a POST request to the OpenRouter API (`https://openrouter.ai/api/v1/chat/completions`), including the user's message and the API key in the headers.
5.  **OpenRouter Response:** OpenRouter processes the request using the specified DeepSeek LLM and sends back a response.
6.  **Backend to Frontend:** The Node.js server forwards the LLM's response (or an error message) back to the frontend.
7.  **Display Response:** The frontend JavaScript receives the response from the backend and displays the bot's message in the chat interface.

## Technology Stack
*   **Frontend:**
    *   HTML
    *   React (via CDN for UI components and state management)
    *   Tailwind CSS (via CDN for styling)
    *   JavaScript (ES6+ with Babel for JSX transpilation in the browser)
    *   Three.js (for the animated background)
*   **Backend:**
    *   Node.js (JavaScript runtime environment)
    *   Express.js (Web application framework for Node.js)
    *   `dotenv` package (for managing environment variables like the API key)
*   **LLM Integration:**
    *   OpenRouter API
    *   DeepSeek Model (e.g., `deepseek/deepseek-chat`)

## Important Security Note
Your `OPENROUTER_API_KEY` is sensitive and provides access to your OpenRouter account.
*   **NEVER** commit the `.env` file to a Git repository if it contains your actual API key. Add `.env` to your `.gitignore` file.
*   **NEVER** embed your API key directly into the frontend JavaScript (`index.html`) or any other client-side code.
*   The API key should only reside in the `.env` file on the server-side, where it is read by `server.js` and is not exposed to the user's browser.

This setup ensures that your API key remains confidential and secure.
