# `react-redux-simple-modal` [![Build Status](https://travis-ci.org/sebinsua/react-redux-simple-modal.png)](https://travis-ci.org/sebinsua/react-redux-simple-modal) [![npm version](https://badge.fury.io/js/react-redux-simple-modal.svg)](https://npmjs.org/package/react-redux-simple-modal)
> A simple modal switcher for React.

A super simple set of actions, a reducer and a component to display modals.

## Install

```sh
npm install --save react-redux-simple-modal
```

## Example

```js
import React from 'react'
import { connect } from 'react-redux'
import { ModalSwitcher, openModal } from 'react-redux-simple-modal'

import ExampleModal from './ExampleModal'
import OtherExampleModal from './OtherExampleModal'
import { EXAMPLE_MODAL, OTHER_EXAMPLE_MODAL } from './constants'

const ExamplePage = ({ openModal }) => (
  <div className="example-page">
    <ModalSwitcher
      modals={{
        [EXAMPLE_MODAL]: ExampleModal,
        [OTHER_EXAMPLE_MODAL]: OtherExampleModal
      }}
    />
    <button onClick={openModal.bind(null, EXAMPLE_MODAL)}>Open Example Modal</button>
    <button onClick={openModal.bind(null, OTHER_EXAMPLE_MODAL)}>Open Other Example Modal</button>
  </div>
)

export default connect(
  null,
  { openModal }
)(ExamplePage)
```

## API

### Reducer

Your root reducer should use the `reducer` exported by this module against its `modals` key.

### Actions

#### `openModal(modalType, modalParams)`

This opens the `SimpleModalComponent` referred to by `modalType`.

`modalType` is a constant that references a component passed into `ModalSwitcher`'s `modals` prop.

`modalParams` are a set of props that you wish to be set on the `SimpleModalComponent`.

#### `closeModal()`

This removes the current modal.

It has no arguments.

### Component

#### `<ModalSwitcher modals={modals} />`

This renders a `SimpleModalComponent` iff a `modalType` that matches a key within `modals` has been set within the modals store.

###### `<SimpleModalComponent modalType={modalType} closeModal={closeModal} modalParams={modalParams} />`

`SimpleModalComponent` describes the contract that your modals should follow.

They should use the `closeModal` prop that was passed in to close themselves.

They will receive the extra props passed in as second argument of `showModal(..., modalParams)` as a `modalParams` prop.
