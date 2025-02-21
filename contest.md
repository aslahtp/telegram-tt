# Introduce the new Chat Folders appearance
- **Fetching and Preparing Data:**
  • During mount, the component sends a loadChatFolders action that retrieves folders data through an API request.
  • The received folder data is normalized into a mapping of folder objects and an ordered array of folder IDs.
  • A special "All Chats" folder is constructed (using useMemo) based on the first folder ID.

- **Rendering Folder Tabs:**
  • The component translates the sorted folder IDs into constructing tab objects for rendering via a TabList.
  • Each tab consists of an icon (based on folder title), optional unread indicators, and context actions (share, edit, delete).
  • Conditions are enforced (e.g., hiding folders over the maximum permitted) and context actions are selectively rendered.

- **Transitions, Animations & User Interactions:**
  • Transitions are managed using a Transition component and hooks (such as useShowTransition) to animate the content when changing the active folder.
  • Keyboard shortcuts (e.g., Ctrl+Shift+Digit) and swipe gestures (using captureEvents) allow fast navigation between folders on desktop and touch devices.
 • Added scrolling support with scrollbar and mouse wheel if the list of folders is long

- **Global State & Integration:**
• The component makes use of higher-order components (withGlobal) and selectors to tap into state like activeFolder, limits, and unread counters.
• ChatFolders is made part of the entire Left Column layout (through LeftMain and LeftColumn) to maintain uniformity with other components (chat list, search, forum panel).

This is how i incorporated into the UI with support for smooth transitions, efficient state updates, and responsive interactions.
# Rework the existing text editor from scratch and eliminate its imperfections:
- **proper support for edit history:** 
	slight changes into the code
- **Add support for editing quotes:** 
	- A dedicated quote button was added to the text formatter’s toolbar. When clicked, it calls a handler that: Retrieves the text to be quoted (for example, from the current message or the user’s selection). Wraps that text in the appropriate quote formatting (for example, by adding a prefix like “> ” or applying specific styling).Inserts the formatted quote into the text input, updating the component’s state accordingly. 
	- Keyboard Shortcut (Ctrl+Q / Cmd+Q ): In parallel,a keyboard shortcut was registered using a hook . This shortcut listens for a specific key combination and, when triggered, calls the same quote handler used by the button. This ensures that users can quickly insert a quote without having to click the button.
- **Add support for Markdown syntax:**
	- **Bold:** surround the text with double asterisks eg: \**this text is bold\**
	- **Italic:** surround the text with double underscore eg: \__this test is italic\__
	- **strikethrough:** surround the text with double tilde characters eg: \~~this test is strikethrough\~~
	- **monospace:** surround the text with single backtick character eg: \`this test is monospace\`
	- **spoiler:** surround the text with double vertical bar eg: \||this test is spoiler\||
	- **Links:** square brackets followed by parentheses. The square brackets hold the text, the parentheses hold the link eg: ```[Link text Here](https://link-url-here.org)```
