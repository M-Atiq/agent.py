# agent
chatboot
from fastapi import FastAPI, Request
from fastapi.responses import HTMLResponse

app = FastAPI()

@app.get("/", response_class=HTMLResponse)
async def home(msg: str = ""):
    reply = ""

    if msg:
        msg = msg.lower()

        # Basic AI-like responses
        if msg in ["hi", "hello"]:
            reply = "Hi there! 👋 How can I help you today?"
        elif "how are you" in msg:
            reply = " but I'm doing great! 😄"
        elif "your name" in msg:
            reply = "My name is Agent. I'm your chatbot assistant."
        elif "bye" in msg:
            reply = "Goodbye! Have a great day! 👋"
        else:
            reply = "Try asking something else."

    return f"""
    <html>
        <head>
            <title>Agent Chatbot</title>
        </head>
        <body>
            <h2>🤖 Agent Chatbot</h2>
            <form action="/" method="get">
                <input type="text" name="msg" placeholder="Ask something..." required />
                <input type="submit" value="Send" />
            </form>
            {"<p><b>You:</b> " + msg + "</p>" if msg else ""}
            {"<p><b>Agent:</b> " + reply + "</p>" if msg else ""}
        </body>
    </html>
    """
