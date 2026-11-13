---
last_updated: 2026-11-11
version: 5.2.0
product_versions:
  ios: "1.0.0"
  android: "1.1.1"
generated_from: "dev-docs/specs/USER_MANUAL_SPEC.instructions.md"
---

# User Manual

## Overview

Text Math is a mental arithmetic practice app. It gives you generated
problems to solve in your head, offers a hint when you need one, and after
each problem shows two different ways to reach the answer so you can compare
methods. The goal is comfort and flexibility with numbers rather than speed
or memorized facts.
<!-- Verified from: platform/ios/text_math/ContentView.swift [HomeView, principleCard] -->
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [WorkoutView] -->

For example, `19 + 28 + 13` does not need to be written out in columns. You
might pair `19 + 13` to make 32 and then add 28, or keep a running total
from left to right. Both are valid, and Text Math shows both.
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [regroupedAddition] -->

Text Math is for anyone who wants to improve their number sense. It may suit
students, but it is not organized around school grades, homework, or test
preparation.

Text Math runs on iPhone, iPad, and Android. Its interface is the app's touch
screen.
<!-- Verified from: platform/ios/text_math.xcodeproj/project.pbxproj [INFOPLIST_KEY_CFBundleDisplayName, TARGETED_DEVICE_FAMILY] -->

## Installation and Setup

### Install on Android

Android requires Android 8.0 or newer. This repository provides an independently
buildable Android project; it is not a Google Play listing. Build and run using
the [Android instructions](../platform/android/README.md). The debug APK
includes development feedback tools and installs separately from a signed
release.

The practice behavior described below also applies to Android: mixed 3/5/10
problem workouts, three attempts, help, two solution methods, quotient and
remainder entry, Good/Bad ratings, and the timer and focus options. The
workout card's button is labeled **Start Session** on Android. Android uses
**Check** to submit and **Next** to move from quotient to remainder.
**Settings** is the gear icon in the top bar. The system Back button and the
close icon (**End workout**) both ask before discarding an active workout;
choose **Keep going** to cancel.

In Android Settings, **Copy ratings to clipboard** copies plain text,
**Share ratings file** opens Android's share chooser with a JSON file, and
**Save ratings file** opens a file picker. File destinations depend on the
providers installed on your device. Ratings and settings are local to each
platform; they do not synchronize between iOS and Android.

Android restores an active workout after rotation or system recreation. The
solve timer includes time spent away from the app and excludes time reviewing
methods. Automatic Android backup and device transfer are disabled. Export
important ratings before clearing app storage or uninstalling. If a saved
ratings archive cannot be read, it remains untouched and new ratings pause;
discarding it in Settings requires confirmation and cannot be undone.

Debug builds include **Feedback** in the top bar, a shake trigger, optional
screenshots, problem feedback notes, and an optional backup folder you select.
Release builds omit those developer controls. Android-specific setup and
feedback retrieval are documented in the
[Android README](../platform/android/README.md). The iOS-specific installation
and operating-system controls below remain labeled for iOS.

### Install on iOS

| Item | Details |
| --- | --- |
| Devices | iPhone and iPad |
| System requirement | iOS 26.5 or later |
| Version | 1.0.0 |
| Installation source | Unknown. The app has not been published, and no download location is available yet. |
| Dependencies | None beyond iOS |
<!-- Verified from: platform/ios/text_math.xcodeproj/project.pbxproj [IPHONEOS_DEPLOYMENT_TARGET, TARGETED_DEVICE_FAMILY, MARKETING_VERSION] -->

No setup is required after installation. The app does not ask for an account,
sign-in, or permissions. You can adjust its options at any time in
**Settings**.
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView] -->
<!-- Verified from: docs/PRIVACY.md [Developer services] -->

## Starting the Program

1. Tap the **Text Math** icon on your Home Screen.
1. The home screen opens with the title **Text Math** and the line
   **Mental math practice**.
<!-- Verified from: platform/ios/text_math/ContentView.swift [HomeView navigationTitle, navigationSubtitle] -->
<!-- Verified from: platform/ios/text_math.xcodeproj/project.pbxproj [INFOPLIST_KEY_CFBundleDisplayName] -->

To quit, leave the app the usual iOS way, such as swiping up from the bottom
of the screen. Your settings and ratings are kept. A workout in progress is
not saved.
<!-- Verified from: platform/ios/text_math/ContentView.swift [ContentView, SettingsView] -->
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences.save] -->

## Getting Around

| Screen | How to get there | What it contains |
| --- | --- | --- |
| Home | Opens at launch | The **Workout** card, the **How it works** steps, and the **Settings** gear button at the top right |
| Workout | Tap a workout card | One problem at a time, a progress bar at the top, and an **X** button to end the workout |
| Review | Answer correctly, or use all three attempts | The answer, a rating question, the solution methods, and **Next problem** or **Finish workout** |
| Workout complete | Finish the last problem | Your score, an optional solve time, and **Return home** |
| Settings | Tap the gear button on the home screen | Ratings export and the app's options; tap **Done** to close |
| Privacy | Tap **Privacy** in Settings | The privacy policy |
<!-- Verified from: platform/ios/text_math/ContentView.swift [HomeView, WorkoutCard, SettingsView] -->
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [WorkoutView toolbar, solvingView, reflectionView, completionView] -->
<!-- Verified from: platform/ios/text_math/PrivacyPolicyView.swift [PrivacyPolicyButton] -->

The app has no separate help screen. While solving, tap **Help** for a hint
about the current problem.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [solvingContent] -->

## Everyday Tasks

### Start a Workout

1. On the home screen, under **Workout**, tap **Start** on the **Mixed
   Practice** card.
1. The workout opens with the first problem.
<!-- Verified from: platform/ios/text_math/ContentView.swift [HomeView.workoutSelection, WorkoutCard] -->
<!-- Verified from: platform/ios/text_math/WorkoutModel.swift [WorkoutSelection] -->

**Mixed Practice** is currently the only workout. Its card reads **Addition,
subtraction, multiplication, division, and fractions.** Below that, it shows
how many problems the workout has, the three attempts you get for each, and
how many problems you have rated so far.

Each time you start it, Text Math creates a new set of problems and mixes the
problem types so that no single operation dominates. A workout has ten
problems unless you choose 3 or 5 under **Problems per workout** in Settings.
Problems you have already rated are skipped, so each workout brings new ones.
<!-- Verified from: platform/ios/text_math/WorkoutModel.swift [WorkoutSelection.subtitle, problemCountChoices, defaultProblemCount] -->
<!-- Verified from: platform/ios/text_math/ContentView.swift [WorkoutCard, Fact] -->
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [generateAll] -->

| Problem type | Example | Strategy it practices |
| --- | --- | --- |
| Three-term addition | `19 + 28 + 13` | Pair two terms that nearly make a multiple of ten, then correct |
| Addition near a round number | `147 + 68` | Round, then compensate; or split by place value |
| Subtraction near a round number | `85 − 37` | Subtract a round number and adjust; or count up |
| Multiplication | `17 × 6` | Split into tens and ones, or round up and subtract |
| Division | `119 ÷ 7` | Split the dividend into known multiples; or use multiplication |
| Division with a remainder | `51 ÷ 6` | Remove whole groups and find what is left over |
| Fraction of a quantity | `3/4 of 68` | Find one equal part first; or subtract the complement |
| Fraction with a larger denominator | `5/6 of 96` | Halve an easier part to reach one part |
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [Family] -->

Every answer is a whole number. Fractions are always shown in lowest terms.
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [fractionOfQuantity, fractionOfLargerQuantity] -->

### Solve a Problem

1. Read the problem under **Problem _N_ of _M_** and work it out in your head.
1. Enter your answer with the on-screen number pad. Tap **⌫** to delete the
   last digit.
1. Tap the arrow button to check your answer.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [solvingContent, NumberPad] -->

Accepted input:

- Digits only, up to five digits in each answer field.
- The arrow button is unavailable until you have entered an answer.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [NumberPad.append, canSubmit] -->

If your answer is wrong, the field clears, a message such as **Not quite — 2
attempts left. Try another method.** appears briefly, and the hint opens
automatically. You have three attempts per problem. After the third wrong
answer, the answer is revealed and you move on to the review.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [submit, solvingContent] -->
<!-- Verified from: platform/ios/text_math/WorkoutModel.swift [WorkoutSession.maxAttempts, submit] -->

### Get a Hint

1. While solving, tap **Help** below the number pad.
1. A short hint for the current problem appears, such as **Replace 58 with 60,
   then compensate.**
1. Tap **Hide help** to close it.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [solvingContent] -->
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [additionCompensation] -->

The hint also opens on its own after a wrong answer.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [submit] -->

### Answer a Division Problem with a Remainder

Some division problems do not divide evenly. These show two fields,
**Quotient** and **Remainder**, separated by **R**.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [answerEntry] -->

1. Enter the quotient.
1. Tap the arrow button to move to **Remainder**, or tap the **Remainder**
   field. While it moves to the next field, the arrow button is yellow and
   its arrow points to a line; it does not check your answer yet.
1. Enter the remainder.
1. Tap the arrow button, now teal again, to check both parts.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [answerEntry, advancesToRemainder, submit, NumberPad] -->

Tap either field to go back and change it. Both parts must be correct for the
answer to count. For `51 ÷ 6`, enter 8 and 3; the answer is shown as `8 R 3`.
<!-- Verified from: platform/ios/text_math/WorkoutModel.swift [WorkoutProblem.accepts, answerText] -->

### Review Solution Methods

After a correct answer the review screen shows **Correct**; after three
missed attempts it shows **Answer revealed**. Both show the full problem with
its answer, such as `17 × 6 = 102`.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [reflectionView] -->

When **Show solution methods after each problem** is on, the screen also shows
two method cards. Each card has a title, such as **Split into tens and ones** or
**Round up and subtract**, numbered steps, and a one-line note on why the method
works.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [reflectionView, ReasoningCard] -->
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [multiplicationDecomposition] -->

Tap **Next problem** to continue, or **Finish workout** on the last problem.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [reflectionView] -->

### Rate a Problem

The review screen asks **Was this a good problem for mental reasoning?**

1. Tap **Good** or **Bad**.
1. The button you tapped fills in, and the line **Saved: Good. You can change
   your rating.** (or **Bad**)
   confirms the rating.
1. To change it, tap the other button.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [reflectionView] -->

A rating judges the problem itself, not whether you solved it or how fast.
Ratings are matched to the problem's text and answer. New workouts skip
problems you have rated, but a problem can still repeat when few new ones of
its type are left. Your earlier rating is then shown with the line **You rated
this problem Good in an earlier workout.** (or **Bad**), and you can change
it.
Text Math keeps your 200 most recent ratings and removes the oldest when that
limit is reached. To export your ratings, see
[Export Your Ratings](#export-your-ratings).
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences.rate, maximumExamples] -->
<!-- Verified from: platform/ios/text_math/WorkoutModel.swift [WorkoutProblem.signature] -->

### Finish a Workout

After the last problem, tap **Finish workout**. The **Workout complete** screen
shows **Solved _N_ of _M_ problems.**, where _M_ is the workout's length, and,
when the solve timer is on, **Solve time:** in minutes and seconds. Tap
**Return home** to go back.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [completionView] -->

The solve time adds up only the time spent solving. Time spent on the review
screens is not counted.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [submit, advance] -->

### End a Workout Early

1. Tap the **X** button at the top left.
1. In **End this workout?**, tap **End workout** to leave, or **Keep going**
   to continue.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [WorkoutView toolbar, confirmationDialog] -->

Ending a workout discards its progress. Ratings you already saved are kept.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [confirmationDialog] -->
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences.rate] -->

### Read the Privacy Policy

1. On the home screen, tap the gear button to open **Settings**.
1. Under **Privacy**, tap **Privacy**.
1. To ask a question, tap **Contact Plain Text Office**, which opens the
   contact page on the developer's website.
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView] -->
<!-- Verified from: platform/ios/text_math/PrivacyPolicyView.swift [PrivacyPolicyView] -->

### Send Feedback

On Android, bug reports and feature requests can be sent from the app.

1. On the home screen, tap the gear button to open **Settings**.
1. Under **About**, tap **Send feedback**.
1. Tap **Report a bug** or **Request a feature**. Your email app opens a draft
   to `support@plaintxtoffice.com` that already contains the app version, the
   Android version and the device model. Write your message and send it.
1. To use the website instead, tap **Open contact form**.

Ratings and problems are never included, and nothing is sent unless you send
it.
<!-- Verified from: platform/android/app/src/main/kotlin/com/plaintxtoffice/textmath/ui/FeedbackScreen.kt; platform/android/app/src/main/kotlin/com/plaintxtoffice/textmath/ui/SettingsScreen.kt -->

## Settings and Preferences

Open **Settings** with the gear button on the home screen, and tap **Done**
to close it. Changes are saved as soon as you make them and are kept between
uses.
<!-- Verified from: platform/ios/text_math/ContentView.swift [HomeView toolbar, SettingsView] -->

| Setting | Default | Accepted values | How to change it |
| --- | --- | --- | --- |
| **Problems per workout** | 10 | 3, 5, or 10 | Segmented control at the top of Settings |
| **Show solution methods after each problem** | On | On or off | Toggle under **After solving** |
| **Show solve timer** | Off | On or off | Toggle under **Timing** |
| **Hide problem after a few seconds** | Off | On or off | Toggle under **Focus** |
| **Hide after** | 5 seconds | 3, 5, 8, or 12 seconds | Picker under **Focus**, shown when **Hide problem after a few seconds** is on |
| **Blind entry** | Off | On or off; always on while **Hide problem after a few seconds** is on | Toggle under **Focus** |
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView, SettingsKey] -->

- **Problems per workout**: sets the length of the next workout you start. A
  workout in progress keeps its length.
- **Show solution methods after each problem**: when off, the review screen
  shows only the answer and the rating question, so you can move straight on.
  The **Help** hint while solving is not affected.
- **Show solve timer**: shows a stopwatch above each problem while you solve
  it and adds the total solve time to the **Workout complete** screen.
- **Hide problem after a few seconds**: replaces the problem with **Problem
  hidden** once the **Hide after** delay passes, so you hold the numbers in
  your head as well as your working. Tap **Show again** to see the problem for
  another delay. While this setting is on, **Blind entry** stays on and cannot
  be turned off, so the answer field cannot be used to store the numbers.
  Workouts started with this setting on leave out three-term addition, which
  would mean holding too many numbers at once.
- **Blind entry**: shows a dot in place of each digit you type, so you commit
  to the whole answer before checking it.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [solvingContent, problemPrompt, reflectionView, completionView, AnswerField] -->
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [generateAll, allowedWhenPromptHidden] -->

The **Problem ratings** section at the top of **Settings** shows how many
rated problems are saved and holds the export buttons described in
[Importing and Exporting](#importing-and-exporting).
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView] -->

## Importing and Exporting

Text Math can export your problem ratings as plain text. It has no import
feature.
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView] -->

### Export Your Ratings

1. On the home screen, tap the gear button to open **Settings**.
1. Under **Problem ratings**, tap one of:
   - **Copy ratings to clipboard** to copy the list. The message **Ratings
     copied. Paste them into any tool to look for patterns.** appears.
     Copying replaces whatever was on the clipboard.
   - **Share ratings file** to send the list as a JSON file named
     `text_math-ratings-<date>-<time>.json` to an app or destination you choose.
     Each rating includes the problem, its answer, when you rated it, its hint,
     and its method names.
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView] -->
<!-- Verified from: docs/PRIVACY.md [Sharing] -->

Both buttons are unavailable until you have rated at least one problem.
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView] -->

The export contains every saved rating, oldest first. It starts with two
lines explaining the labels and giving the totals and export date, followed
by a blank line. Each rating is then one line: `good` or `bad`, a tab, and
the problem with its answer.
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences.exportText] -->

```text
Mental arithmetic problems I rated. "good" means a good problem for mental reasoning; "bad" means it was not.
2 rated (1 good, 1 bad). Exported Oct 26, 2026.

good	19 + 23 + 11 = 53
bad	51 ÷ 6 = 8 R 3
```

The export date follows your device's date format. Text Math does not
analyze your ratings itself. Paste the list into a tool of your choice, such
as a spreadsheet or an AI assistant, to look for patterns in the problems you
rated well.
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences.exportText] -->
<!-- Verified from: docs/PRIVACY.md [On your device] -->

## Commands and Shortcuts

Text Math is controlled with on-screen buttons. It has no menus and defines
no keyboard shortcuts.
<!-- Verified from: platform/ios/text_math/ContentView.swift -->
<!-- Verified from: platform/ios/text_math/WorkoutView.swift -->

| Control | Where | What it does |
| --- | --- | --- |
| Gear button | Home screen, top right | Opens **Settings** |
| **Start** | Home screen, workout card | Starts the workout |
| **0** to **9** | Number pad | Enters a digit |
| **⌫** | Number pad | Deletes the last digit |
| Arrow button | Number pad | Checks the answer (teal), or moves from **Quotient** to **Remainder** (yellow) |
| **Help** / **Hide help** | Below the number pad | Shows or hides the hint |
| **X** button | Workout, top left | Asks whether to end the workout |
| **Good** / **Bad** | Review screen | Rates the problem |
| **Next problem** / **Finish workout** | Review screen | Moves on |
| **Return home** | Workout complete screen | Returns to the home screen |
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [NumberPad, solvingContent, reflectionView, completionView, toolbar] -->
<!-- Verified from: platform/ios/text_math/ContentView.swift [HomeView toolbar] -->

## Your Data Files

Text Math has no files for you to open or edit. It stores your settings and
your 200 most recent ratings, including each rated problem, in the app's own
storage on your device. Problems are generated on your device, and ratings
are not sent to any AI service.
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences] -->
<!-- Verified from: docs/PRIVACY.md [On your device] -->

There is no control to clear all ratings. Deleting the app removes its
ratings and settings. Copies you exported and device backups are separate.
<!-- Verified from: docs/PRIVACY.md [Removing data] -->

## Troubleshooting

| Symptom | Likely Cause | Resolution |
| --- | --- | --- |
| The arrow button cannot be tapped | No answer has been entered, or the remainder is still empty | Enter the answer, and for remainder problems fill in both fields |
| More digits cannot be entered | Each answer field holds at most five digits | Tap **⌫** to correct the answer |
| The review screen shows **Answer revealed** | All three attempts were used, so the answer was shown | Study the methods on the review screen, then continue |
| The review screen shows no methods | **Show solution methods after each problem** is off | Turn it on in **Settings** |
| No stopwatch or solve time appears | **Show solve timer** is off | Turn it on in **Settings** |
| The problem is replaced by **Problem hidden** | **Hide problem after a few seconds** is on | Tap **Show again**, or turn the setting off in **Settings** |
| Your answer shows only dots | **Blind entry** is on | Turn it off in **Settings** |
| **Blind entry** cannot be turned off | **Hide problem after a few seconds** is on | Turn off **Hide problem after a few seconds** first |
| **Copy ratings to clipboard** and **Share ratings file** are unavailable | No problems have been rated yet | Rate a problem on a review screen, then try again |
| **Settings** shows **Saved ratings could not be read. A backup of the original data was kept and new ratings are paused.** | The saved ratings could not be loaded, so new ratings are not saved | Tap **Discard unreadable ratings and start fresh** to start a new ratings list |
| **Settings** shows **Could not save ratings.** | Saving the ratings list failed | Unknown. |
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [canSubmit, NumberPad.append, reflectionView, AnswerField] -->
<!-- Verified from: platform/ios/text_math/WorkoutModel.swift [WorkoutSession.submit] -->
<!-- Verified from: platform/ios/text_math/ContentView.swift [SettingsView] -->
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences.init, discardUnreadableRatings, save] -->

## FAQ

### Does a Wrong Answer Affect My Rating?

No. Ratings judge whether the problem was good for mental reasoning, apart
from whether you solved it or how long it took.
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [reflectionView] -->
<!-- Verified from: platform/ios/text_math/ProblemPreferences.swift [ProblemPreferences.rate] -->

### Will I See the Same Problems Every Time?

No. A new set of problems is generated each time you start a workout, and
problems you have rated are skipped. A problem can still repeat when few new
ones of its type are left; if you rated it before, your rating is shown.
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [generateAll] -->
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [reflectionView] -->

### Is My Workout Score Saved?

No. The **Workout complete** score is shown at the end of the workout and is
not stored. Only settings and ratings are saved.
<!-- Verified from: platform/ios/text_math/WorkoutModel.swift [WorkoutSession] -->
<!-- Verified from: docs/PRIVACY.md [On your device] -->

### Does Text Math Need an Account or Internet Connection?

No account is used, and problems are generated on your device. Sharing your
ratings and the **Contact Plain Text Office** link use other apps or the web.
<!-- Verified from: docs/PRIVACY.md [On your device, Sharing, Developer services] -->
<!-- Verified from: platform/ios/text_math/PrivacyPolicyView.swift [PrivacyPolicyView] -->

## Glossary

| Term | Meaning |
| --- | --- |
| Workout | A set of 3, 5, or 10 generated problems solved one at a time |
| Hint | A short, problem-specific nudge shown by **Help** |
| Solution method | One of two step-by-step ways to reach a problem's answer |
| Compensate | Adjust an answer after rounding a number to make the problem easier |
| Quotient | The whole-number result of a division |
| Remainder | What is left over when a division does not come out evenly |
| Rating | Your **Good** or **Bad** judgment of a problem |
| Blind entry | An option that hides your digits as you type |
<!-- Verified from: platform/ios/text_math/WorkoutView.swift [solvingContent, reflectionView, AnswerField] -->
<!-- Verified from: platform/ios/text_math/MentalMathProblemGenerator.swift [Family] -->
