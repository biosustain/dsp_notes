# Graphical User Interfaces

We built graphical user interfaces (GUIs) for some of our tools to make them easier
to use for non-technical users who focus mainly on the lab.

We use mainly Streamlit. Other options in the Python ecosystem are
listed below. Generally, all frameworks should offer a Python API.

## General Guidelines

- Managing state is important and hard.
- An app should have a single responsibility; it should do one thing mainly.


## Frameworks

- streamlit
- gradio
- panel
- django

### [Streamlit](https://streamlit.io/)

- Easy to start sketching a GUI.
- Each time a user changes an input, the whole app is re-run (a single page).
  - Use forms to avoid re-runs and gather several inputs at once.
- Multiple tabs are still one page.
- Multi-page apps are multiple apps that share an overall state dictionary.
  - Widget values are by default reset when switching pages, see
    [concepts/multipage-apps/widgets](https://docs.streamlit.io/develop/concepts/multipage-apps/widgets).
  - For detailed explanations on widget behavior, see
    [concepts/architecture/widget-behavior](https://docs.streamlit.io/develop/concepts/architecture/widget-behavior).
    - If a widget is not displayed, its state is erased.
- Real-time things are hard, but check out [streamlit-webrtc](https://github.com/whitphx/streamlit-webrtc).
- By default, re-execution is from top to bottom.
  - Forms let you gather several inputs at once before a button starts the computation.
  - Components can be used to limit re-execution to a part of the app.
  - Use `st.cache_data` to cache results of expensive operations and share them between all sessions (users).
  - See [caching](https://docs.streamlit.io/develop/concepts/architecture/caching).
  - Caching respects different arguments.
- Components in Streamlit can be created from basically any JavaScript library.
  - See [Streamlit components](https://docs.streamlit.io/library/components).
  - See [Streamlit component template](https://github.com/streamlit/component-template).
- Session state idiosyncrasies:
  - Components can update the session state, but an update in the session state is not reflected in the component.
  - Callbacks on components can be used to update the session state.
  - Sidebar widgets are shared across pages (and are always visible) - avoid using session state.
- Callbacks: 
  - `on_click` argument of buttons: run callback before page is rerun
  - `if` class with direct invocation allows to choose when to run the callback
- use `st.empty` to define the order of widgets before you actually create these. Use
  the container initialized by `st.empty()` later to populate it.


Material:

- For 5 limitations to be aware of, see
Fanilo Andrianasolo's [video](https://www.youtube.com/watch?v=IOYHVPPbZII).
- Advanced: Adding custom components from JavaScript, see [video](https://www.youtube.com/watch?v=TqOGBOHHxrU).
