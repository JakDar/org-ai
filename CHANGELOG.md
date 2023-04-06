# Changelog

## [0.2.5] - 2023-04-07
- Another attempt to fix unicode / multi-byte inputs. The string encoding we had before 0.2.3 was correct, but I missed that the entirety of the request body needs to be encoded as utf-8, including the headers need to be utf-8. In my case my openai auth token was not utf-8, and so i got a `Multibyte text in HTTP request` and wrongly assumed this is due to the content. This should be fixed now.

## [0.2.4] - 2023-04-04
### Changed
- Make 'org-ai-summarize' treat the region as text not as code (https://github.com/rksm/org-ai/pull/22)
- fix "Error on checkbox C-c C-c after org-ai loaded" (https://github.com/rksm/org-ai/issues/23)

## [0.2.3] - 2023-04-04
### Changed
- correctly encode UTF-8 strings when sending them to the API. This should fix non-ascii characters and multi-byte characters such as emojis in the input.
- start markdown codeblock AI responses on their own line (see https://github.com/rksm/org-ai/issues/17#issuecomment-1494970605)

## [0.2.2] - 2023-03-31
### Changed
- add `"ai"` to `org-protecting-blocks` to fix the block syntax highlighting.

## [0.2.1] - 2023-03-30
### Added
- `org-ai-switch-chat-model`
### Changed
- No max-tokens in ai snippet
- modified global shortcuts:
    - `C-c M-a r`: `org-ai-on-region`
    - `C-c M-a c`: `org-ai-refactor-code`
    - `C-c M-a s`: `org-ai-summarize`
    - `C-c M-a m`: `org-ai-switch-chat-model`
    - `C-c M-a !`: `org-ai-open-request-buffer`
    - `C-c M-a $`: `org-ai-open-account-usage-page`
    - `C-c M-a t`: `org-ai-talk-input-toggle`
    - `C-c M-a T`: `org-ai-talk-output-toggle`
### Removed
- Make greader dependency optional

## [0.2.0] - 2023-03-30
### Added

#### Speech input/output. Talk with your AI!
- In org-mode / `#+begin_ai..#+end_ai` blocks:
  - `C-c r` to record and transcribe speech via whisper.el in org blocks.
- Everywhere else:
    - Enable speech input with `org-ai-talk-input-toggle` for other commands (see below).
- Enable speech output with `org-ai-talk-output-enable`. Speech output uses os internal speech synth (macOS) or `espeak` otherwise.

#### Non-org-mode commands
- `org-ai-prompt`: prompt the user for a text and then print the AI's response in current buffer.
- `org-ai-on-region`: Ask a question about the selected text or tell the AI to do something with it.
- `org-ai-summarize`: Summarize the selected text.
- `org-ai-explain-code`: Explain the selected code.
- `org-ai-refactor-code`: Tell the AI how to change the selected code, a diff buffer will appear with the changes.

#### Other improvements
- In org-mode / `#+begin_ai..#+end_ai` blocks:
    - Press `C-c <backspace>` (`org-ai-kill-region-at-point`) to remove the chat part under point.
    - `org-ai-mark-region-at-point` will mark the region at point.
    - `org-ai-mark-last-region` will mark the last chat part.

#### Other commands
- `org-ai-open-account-usage-page` show how much money you burned.
- `org-ai-install-yasnippets` install snippets for `#+begin_ai..#+end_ai` blocks.
- `org-ai-open-request-buffer` for debugging, open the request buffer.

## [0.1.4] - 2023-03-17
### Added
- Support for retrieving `org-ai-openai-api-token` from `authinfo` file.

## [0.1.3] - 2023-03-13
### Added
- org-ai yasnippets
### Changes
- Correctly utf decode/encode input/output.
- Set mark before inserting output. This allows to quickly select the output with `C-x C-x`.
- Fix parsing messages that contain a `:`.

## [0.1.2] - 2023-03-08
### Fix ChatGPT prompts
- Add `org-ai-default-chat-system-prompt`, `org-ai-default-inject-sys-prompt-for-all-messages`, `:sys-everywhere` option and allow specifying custom per-block `[SYS]:` system prompts.
- Correctly assign system, user, assistant roles (see https://platform.openai.com/docs/guides/chat/introduction). Before I mixed up system/assistant roles.

## [0.1.1] - 2023-03-06
### Initial release
`#+begin_ai...#+end_ai` blocks that can be used for:
- chatgpt input / output
- "normal" text completion with older gpt models
- image genration (text -> image)

`org-ai-image-variation` command to generate variations of an image.
