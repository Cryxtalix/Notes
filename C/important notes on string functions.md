# Important notes on safe(r) string functions

## strncpy()
* Allows specifying a size.
* Will overwrite strings already in the buffer.
* A longer string will be truncated to the specified size. 
* A shorter string will be null padded to the specified size.
* If string is not one less than the specified size, there will be no \0.
* Specifying (size - 1) for a large string is still insufficient as \0 will still be missing. \0 has to already exist at the last position or be manually inserted.
* TLDR: Only prevents writing beyond the specified size. Ensuring the existence of \0 is up to the user.

## snprintf()
* Allows specifying a maximum length of string to be written to.
* Allows formatting and joining multiple strings together.
* Will overwrite strings already in the buffer.
* A longer string will be truncated to the specified size - 1, and \0 at the last position.
* A shorter string will have \0 at the end of the string, but no further padding.
* Can be certain that \0 will always be written somewhere within the specified size.
* Cannot include the string already in the source in the formatting.
* Might be slower than strcpy family of operations.
* TLDR: Besides the performance issue, seems to work very well.

## strcat()
* Concatenates to an existing string and does not take size into account.
* Will gladly overwrite neighbouring memory addresses.
* Will always include \0 at the end, so the string might still temporarily work as expected. The overwritten memory segments might eventually cause an error.
* TLDR: Dangerous to use without a lot of checking.

## strncat()
* Allows specifying a maximum size of string to be concatenated.
* A longer string will be truncated to the specified size, with \0 appended to the end. The resultant string is one greater than the specified size.
* If specified length of string after concatenation is longer than the buffer, it will gladly overwrite neighbouring memory addresses.
* Will always include \0 at the end, so the string might still temporarily work as expected. The overwritten memory segments might eventually cause an error.
* TLDR: The specified maximum size must be carefully calculated to prevent overflow. It must account for the \0 which will be written even if the maximum size is reached, and might cause an error.
