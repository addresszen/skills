# Messages

Address Lookup uses a small default set of messages to communicate specific events to the user.  All of Address Lookup's default messages can be overridden. They are outlined below:

## Initial Message

`msgInitial`

Displays when the Address Lookup is opened and the input field is empty.

Defaults to `"Start typing to find address"`

## Accessibility (Screen Reader) Message

`msgList`

The aria-label assigned to the address suggestion list. This message will only be picked up by screen readers.

Defaults to `"Select your address"`

## No Match

`msgNoMatch`

Displays when no suggestions could be found for the query.

Defaults to `"No matches found"`

## Unhide Label

`msgUnhide`

Displayed to the user if Address Fields have been hidden. It is shown as a clickable element to trigger manual address entry.

Defaults to `"Enter address manually"`

## Fallback Message

`msgFallback`

Shown when Address Lookup is unable to provide suggestions for any reason (e.g. key is not available).

Defaults to `"Please enter your address manually"`

> **Accessibility**
> 
> Keep in mind these messages are also important for users who rely on the screen-reader. When altering the message be sure that the necessary meaning and intent is understandable to visually impaired users who will be getting audio cues from their screen-reader.
