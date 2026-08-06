
**whatever report month is selected**:

For report month `X`:

- Admission date in `X` = `NEW`
- Admission date in `X - 1 month` = `NEW`
- Admission date before `X - 1 month` = `EXISTING`
- Child status `2` = `WITHDRAWAL`
- Child status `3` archive = not shown

Examples:

- June report: June + May = `NEW`; April or before = `EXISTING`
- July report: July + June = `NEW`; May or before = `EXISTING`
- August report: August + July = `NEW`; June or before = `EXISTING`


