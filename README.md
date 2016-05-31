# draft-js-table

[![NPM version](https://badge.fury.io/js/draft-js-table.svg)](http://badge.fury.io/js/draft-js-table)

`draft-js-table` is a collection of utilities to edit tables in DraftJS.


### Installation

```
$ npm install draft-js-table
```

### Usage

```js
var Draft = require('draft-js');
var TableUtils = require('draft-js-table');


// Insert a new table to replace current block
var newEditorState = TableUtils.insertTable(editorState, nRows, nColumns);

// Insert a new row into the current table
var newEditorState = TableUtils.insertRow(editorState, nRows, nColumns);
```

##### Handle key events inside a table

`draft-js-table` provides a set of functions to help handle key events/commands from DraftJS. This function can be composed with other command handlers.

```js
var MyEditor = React.createComponent({
    getInitialState: function() {
        return {
            editorState: Draft.EditorState.createEmpty()
        };
    },

    onChange: function(editorState) {
        this.setState({
            editorState: editorState
        });
    },

    handleKeyCommand: function(command) {
        var newState = (TableUtils.hanldeKeyCommand(editorState, command)
            || Draft.RichUtils.handleKeyCommand(editorState, command));

        if (newState) {
            this.onChange(newState);
            return true;
        }
        return false;
    },

    render: function() {
        retur  <Draft.Editor
            editorState={this.state.editorState}
            handleKeyCommand={this.handleKeyCommand}
            onChange={this.onChange}
        />;
    }
});
```

