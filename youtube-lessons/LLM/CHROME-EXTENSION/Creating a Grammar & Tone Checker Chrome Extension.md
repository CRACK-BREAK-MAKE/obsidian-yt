![[intro-improve-grammar 1.gif]]




---


Let's build a **Chrome extension** that uses **LLMs (Large Language Models)** to improve grammar and tone.

This tutorial will focus on two key parts:  
1️⃣ Setting up the **manifest file**, the heart of any Chrome extension.  
2️⃣ Integrating the **LLM logic** to process user input.

Let’s dive right in!

---

**[Section 1: The Manifest.json]**

Every Chrome extension starts with the **manifest file**. It’s like a blueprint for your extension. Here’s how ours looks:
![[manifest-explanation.gif]]
🔑 **Key Points to Highlight**:
1. **Manifest Version**: We’re using version 3, the latest version for Chrome extensions.
2. **Permissions**:
    - `host_permissions`: Allows us to communicate with our local LLM service running at `http://127.0.0.1:11434`.
3. **Background Service Worker**: This is where the extension logic runs in the background.
4. **Content Security Policy (CSP)**: This section defines security rules for how scripts and objects (like plugins) are loaded.
	1. 🔹 script-src 'self': This means that only scripts from your own extension can be executed. You cannot load external scripts from the internet (like from a CDN).
	💡 Example:
		✅ Allowed: <script src="script.js"></script> (if script.js is inside your extension)
		❌ Blocked: <script src="https://example.com/script.js"></script>
	2. 🔹 object-src 'self':  This controls where your extension can load plugin-based content. Here, 'self' means that only objects from your extension are allowed, blocking external ones for security.
	💡 Example:
		✅ Allowed: <embed src="plugin.swf"> (if plugin.swf is inside your extension)
		❌ Blocked: <embed src="https://example.com/plugin.swf">
5. **Default Action**: This sets up the popup window and the icon to be used by the plugin

---

**[Section 2: Using LLM with extension]**
![[Screenshot 2025-01-29 at 12.20.27 PM.png]]
---
```commandline

### Dear [Recipient],

I hope this message finds you well.

Best regards,
[Your Name]
```

**[Section 3: Outro]**
And that’s it! 🎉 You’ve just built a Chrome extension powered by LLMs. This setup can be extended further to support more use cases like summarization or translation etc.
![[profile-like-subs.gif | 400]]
If you found this tutorial helpful, don’t forget to **like, comment, and subscribe**! Let me know in the comments if you’d like more tutorials like this.

See you in the next video. Until then, happy coding! 💻✨

---

Would you like me to create visuals or additional detailed explanations for any part?