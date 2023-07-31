# react-blockly-playground

[![Built on Blockly](https://tinyurl.com/built-on-blockly)](https://github.com/google/blockly)

A React Wrapper for using Blockly, the visual programming editor from Google I wrote react-blockly-playground for an internal platform at Tekie to cater student's curriculum activity. 

Features:

* Provides a hook as well as a function component for ease of use + flexibility
* Supports the JSON toolbox format
* Automatically propagates prop updates to Blockly
* Provides callbacks for workspace injection, disposal, changes, and XML import errors
* Automatically generates workspace XML, debounced for performance

## Installation

To add react-blockly to a React app that uses npm, run:

```bash
npm install --save react-blockly-playground
```

## How to use

You can use react-blockly as either a component or a hook.

### As component

Write `import { BlocklyWorkspace } from 'react-blockly-playground';` in your code and use BlocklyWorkspace as a component.

Example:

```jsx
import { BlocklyWorkspace } from 'react-blockly';

function MyBlocklyEditor() {
  const [xml, setXml] = useState();

  return (
    <BlocklyWorkspace
      useDefaultToolbox
      customTools={[tool1]}
      toolboxConfiguration={MY_TOOLBOX} // this must be a JSON toolbox definition
      workspaceConfiguration={WORKSPACE_CONFIGURATION}
      initialXml={xml}
      onXmlChange={setXml}
      onWorkspaceChange={(workspace) => {}}
      onInject={(e) => {}}
      customTheme={Blockly.Theme.Playground}
      blocklyKey='One'
    />
  )
}
```

### Using the hook

Write `import { useBlocklyWorkspace } from 'react-blockly-playground';` in your code and use this hook to inject a Blockly workspace into your rendered components.

Example:

```jsx
import { useBlocklyWorkspace } from 'react-blockly-playground';

function MyBlocklyHookEmbed() {
  const blocklyRef = useRef(null);
  const { workspace, xml } = useBlocklyWorkspace({
    ref: blocklyRef,
    toolboxConfiguration: MY_TOOLBOX, // this must be a JSON toolbox definition
    initialXml: xml,
  });

  return (
    <div ref={blocklyRef} /> // Blockly will be injected here
  )
}
```