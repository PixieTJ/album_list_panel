# Album List Panel WebView Experiment

This branch is a safe playground for testing whether Album List Panel's existing media-library/tree model can drive a custom WebView2 UI.

## Branch

`experiment/webview-library`

## Initial architecture finding

The existing component already separates much of the useful backend from the native Windows tree renderer:

- `main_tree_builder.cpp` builds the hierarchy from foobar2000 media-library track handles, title-format strings and the filter query.
- `Node` stores the hierarchy, child nodes and the `metadb_handle_list` represented by each node.
- `TreeViewPopulator` renders that node model into the native Win32 TreeView.

The first goal is to preserve the current library/tree logic and prove that a second renderer/bridge can consume the same `Node` model without changing normal Album List behaviour.

## Test order

1. Build the fork unchanged and verify it loads in foobar2000.
2. Give the experimental panel an obvious visible name so the test build cannot be confused with upstream.
3. Add a read-only node-tree exporter/bridge.
4. Render the exported model in a minimal WebView2 view.
5. Only after that, wire selection and playback/playlist actions back to foobar2000.

No experimental changes should be made directly on `main`.
