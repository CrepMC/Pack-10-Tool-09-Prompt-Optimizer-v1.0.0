# 06 — Character Limit Engine

Default target:
3800 characters.

Hard max:
4000.

Count the exact final string that will be sent, including:
block labels, spaces, punctuation and merged negative text.

Never rely on approximate token count.

If > target:
compress safely.

If >4000 after safe compression:
BLOCK, do not send.
