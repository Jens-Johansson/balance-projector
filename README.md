# balance-projector

One page javascript app to make account balance projections into the future, with a chart. Uses a very freeform text format for input.

### Features

Project future financial events into an account balance chart. You can type hypotheticals and see directly what happens. One page javascript app. Nothing leaves your browser, for privacy. Stores the input text in a local session in your own browser's localstorage, if you navigate away from the page the text will be there when you return (without eg cookies or some kind of sign up). It also has a preset mechanism in order to handle multiple projection scenarios. Dark mode, built in PNG export, a syntax helper, togglable text labels and an accordion display of the financial events sorted by time. Leverages chart.js. There is a demo [here](https://jens.org/b/) but you could also host this yourself of course.

### Format of the text

|Text|What it does|
|---|---|
|YYYY|Sets the year for subsequent date-spec lines. Until the next YYYY.|
|date-spec: amount comment|A financial event, positive or negative|
|date-spec: amount [monthly] comment|Same but it's recurring regularly|
|date-spec: amount commenty [monthly] mc commentyface|Pretty relaxed parsing so this also works|
|text|Freeform comment text which applies to the subsequent date events|
|unit: currency-unit|Currency unit text strictly for the display. Default is €.|
|# comment|A comment which is just discarded (`#  //  --   ;  %  '  rem` work)|

_YYYY_ is just the year, like `2026`. _date-spec_ is pretty freeform, `nov`, `nov 2`, `2026-05-11` all work. A month without a number is just considered to be mid-month. Dates don't have to be in chronological order. The _amount_ is evaluated angebraically so `-(12 * 7 + 13)` works. In case of ambiguity here `#` ends the algebraic expression so `nov 2: 1+1 # + 4 ` does what you think it would. The recurrence specification is pretty free form too so `[monthly]`, `[42 days]`, or `[2 weeks]` all work.

### An example 

```
unit: k€

2026
summer
aug 29: 5 account balance

sep: -1 bills
oct: -1 more bills

winter is coming
# or maybe not
dec: 2*1.7 + 2 some income from selling stuff

2027
mar 1: -0.5 [monthly]

may 20: -15 need to buy stuff oh noes
jun 12: 10 win lottery, yay
sep 12: 1.2 somehow randomly get money [12 days]

here be dragons
oct 12: 4 another lottery win amazing
```

### What that would generate 

![example chart](https://jens.org/b/balance-projection-example.png)

### Demo

https://jens.org/b/  (no signup, cookies, tracking, or data collection)

### Provenance and license

Yes this was heavily vibe coded, since javascript is a language I don't know well and trying to become more familiar with. Initially using Claude Opus 5 (expensive.. more than $2) and then bugs corrected/ fixed/ enhanced using Qwen3.7+ and GLM5.2. All done from within a [Kagi](https://www.kagi.com "Paid search so you are the customer and not the product") subscription using leftover end of month AI tokens and then some chopping and pasting. BSD 2-clause license, would be anyway but expecially [sic] because vibe coded.

