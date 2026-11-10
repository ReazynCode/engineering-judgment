# CSV example — optional framework reminder

This is a separate learning reference, not an answer template for the active feature. Display only on explicit request. Return to the same exercise afterward without adapting these questions.

**Feature: Users can upload CSV files containing historical stock prices.**

## Requirements

- What file formats and column names are supported?
- What happens if timestamps or prices are missing?
- How large can a file be?

## Architecture

- Should parsing happen in the browser or backend?
- Should the original file be stored?
- Should uploads be processed synchronously or asynchronously?

## Failure Modes

- What if the upload stops halfway through?
- What if the same file is uploaded twice?
- What if the CSV contains malformed or malicious content?

## Tradeoffs

- Is a background queue necessary for expected file sizes?
- Would direct database storage be simpler?
- Which decisions are expensive to reverse?

## Verification

- What tests cover malformed rows?
- How do we verify imported prices match the source?
- Can we reproduce and diagnose a failed import?
