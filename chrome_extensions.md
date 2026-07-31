## Installed Extensions & Purpose

1. React Developer Tools
It allows me to inspect the React component hierarchy in the browser, view component props/state in real-time, and trace performance issues related to unnecessary re-renders.

2. Redux DevTools
Essential for debugging application state changes. It provides a powerful time-travel debugging feature, allowing me to watch every action dispatched and see exactly how the global state morphs over time.

3. JSON Viewer (JSON Formatter)
When inspecting raw API responses directly in the browser, the data is usually unreadable. This extension automatically pretty-prints, syntax-highlights, and makes JSON data collapsible for efficient backend analysis.

4. Lighthouse
Accessible directly within Chrome DevTools, it serves as an automated auditing tool for measuring web page performance, accessibility, SEO, and progressive web app standards.

## The most useful thing I learned
The most useful thing I learned today is how much debugging power can be moved directly into the browser. Before utilizing these tools, debugging global state or checking deeply nested component trees meant littering the codebase with countless `console.log()` statements. 

Learning how to leverage **Redux DevTools** for time-travel debugging completely changes the game—being able to step backward and forward through UI actions to see exactly where data breaks makes troubleshooting state logic significantly faster and less stressful.