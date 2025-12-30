
import gradio as gr

# -----------------------------------
# Simple Memory (like context)
# -----------------------------------
memory = {
    "last_name": None
}

# -----------------------------------
# Core Logic Function
# -----------------------------------
def smart_assistant(user_input):
    text = user_input.lower().strip()

    # Case 1: User enters a name
    if text.isalpha() and len(text.split()) == 1:
        memory["last_name"] = user_input.title()
        return (
            "### 🤖 Answer\n\n"
            f"👤 **{memory['last_name']}**\n\n"
            "Main aap ki kya help kar sakta hoon?\n\n"
            "Aap likh sakte hain:\n"
            "- *is ke bare mein thori information do*"
        )

    # Case 2: User asks for information
    if "information" in text or "bare mein" in text or "batao" in text:
        if memory["last_name"]:
            name = memory["last_name"]
            return (
                "### 🤖 Answer\n\n"
                f"**Name:** {name}\n\n"
                f"{name} aik positive aur motivated personality hai. "
                "Yeh learning, self-growth aur communication mein interest rakhta hai. "
                "Aksar aise log technology, creativity ya professional development "
                "ki taraf attract hotay hain.\n\n"
                "📌 *Yeh information general hai aur sirf demo purpose ke liye hai.*\n\n"
                "👉 Main aur kis tarah aap ki madad kar sakta hoon?"
            )
        else:
            return (
                "### ❌ I don't know\n\n"
                "Pehle kisi ka naam likhein, phir us ke bare mein poochain."
            )

    # Greeting
    if text in ["hi", "hello", "hey", "salam", "assalam o alaikum"]:
        return (
            "### 🤖 Answer\n\n"
            "👋 Hello!\n\n"
            "Aap kisi bhi person ka **naam** likh sakte hain."
        )

    # Default (out of scope)
    return (
        "### ❌ I don't know\n\n"
        "Main sirf naam ya us ke bare mein information provide kar sakta hoon.\n\n"
        "مثال:\n"
        "- Ali\n"
        "- is ke bare mein thori information do"
    )

# -----------------------------------
# UI (Same RAG-Style Look)
# -----------------------------------
custom_css = """
body {
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
}
.answer-box {
    background: #111827;
    border-radius: 16px;
    padding: 20px;
    color: #E5E7EB;
    font-size: 16px;
}
"""

with gr.Blocks(css=custom_css) as demo:
    gr.Markdown(
        """
        # 📚 Smart Assistant (Demo Mode)
        ### ⚡ RAG-Style Output • Logic-Based • No API
        """
    )

    question = gr.Textbox(
        label="💬 Ask something",
        placeholder="Naam likhein ya information poochain...",
        lines=2
    )

    answer = gr.Markdown(
        elem_classes=["answer-box"]
    )

    btn = gr.Button("🚀 Ask", variant="primary")

    btn.click(
        fn=smart_assistant,
        inputs=question,
        outputs=answer
    )

demo.launch()
# If you want the latest version
pip install gradio

# Or with specific version
pip install gradio==3.41.2
https://huggingface.co/spaces/gazar12/college-student-analyzer/blob/main/requirement.txt
