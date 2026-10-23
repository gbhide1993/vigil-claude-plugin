# Vigil Privacy Policy

Vigil runs on your own computer. This page describes what it and its Claude plugin do with data.

## What Vigil records
Vigil records file changes, process starts (with their command text, where secrets are redacted on a best-effort basis) and changes to credential files. File paths and command text can contain personal information such as your username. This data is stored in a local database on your machine.

## What leaves your machine
By default, nothing. Vigil has no telemetry, no update check and no license server call. Two optional features are off until you turn them on in Settings:
- Daily summary webhook: sends the daily summary text to the URL you set.
- External timestamp: sends only a 32-byte hash of an anchor to the timestamp service you set. No events, file paths or names are sent.

## The Claude plugin
The plugin connects only to the local Vigil backend at 127.0.0.1:7422 and reads session summaries from it. The plugin stores nothing and sends nothing to us. What it reads becomes part of your Claude conversation, which is covered by Anthropic's own terms and privacy policy.

## Deleting your data
Uninstall Vigil and choose to delete its data when asked, or delete the Vigil data folder under %LOCALAPPDATA%\V-LAW.

## Contact
girish@getvvault.com
