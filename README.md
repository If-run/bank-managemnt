# Bank & OD Control — monthly statement → management system (v1.0)

One file, **`index.html`**. Open it in Chrome or Edge and it works. There is no server, no login and no monthly cost.

| File | What it is |
|---|---|
| `index.html` | The complete system |
| `sample-statement-HNB-Aug2026.csv` | A test statement (made-up data) to try the upload with |

---

## 1. Start (2 minutes)
1. Double-click `index.html`, **or** put it on GitHub Pages like your other tools. Upload it to a repo, then go to Settings → Pages → main.
2. Press **Load demo data**. You get 6 months of statements, this month to date, and upcoming commitments. With these you can see every screen, including an OD breach warning.
3. Try **Upload statement** with the sample CSV.
4. When you're ready for real data, go to **Settings → Delete all data** and start clean.

The page needs internet the first time it opens, to load its readers and charts. After that the browser keeps them.

## 2. Every month (5 minutes)
1. **Download the statement from online banking.** Choose **CSV or Excel** if the bank offers it, because PDF is the least reliable format.
2. **Upload statement** → choose the file. The system then:
   - reads the file and finds the columns
   - detects the account and the period
   - checks that **opening + credits − debits = closing**
   - marks duplicates
   - classifies the transactions
3. Check the preview:
   - **Green "Statement reconciles"**: good, go ahead.
   - **Red "Reconciliation error"**: something is wrong. Press **Map columns** and fix which column is which, until it turns green.
4. Give each **Needs review** line a category. Tick *remember* so the same kind of line is classified automatically next month.
5. **Confirm import.** The monthly report opens.
6. Update **Commitments**, which are what you expect to come in and go out. Mark items **Done** once they show in the bank.
7. Open **Action center** and review it.
8. Go to **Settings → Download backup**.

## 3. First-time setup
- **Settings → Bank accounts:** enter each account's **approved OD limit**. Without it, OD % and breach warnings can't be calculated.
- **Settings → General:** enter the company name and the financial-year start month. It is set to **April** by default (the Sri Lankan tax year).
- **Commitments:** enter the collections you expect, the cheques you have received or issued, and scheduled payments. Tick **flexible** on payments whose date could move, such as supplier payments. The OD analysis only suggests moving flexible items.

## 4. The four kinds of data
Every figure carries a badge, so nobody confuses a plan with a fact:
- **ACTUAL**: from imported bank statements
- **EXPECTED**: committed but not yet in the bank (collections due, cheques received or issued)
- **PLANNED**: management's plan (scheduled payments)
- **FORECAST**: calculated by the system

## 5. Things to know
- **Data lives in this browser on this PC.** Another PC or browser won't see it, so keep one "finance PC". Clearing browser data erases it, which is why you should back up every month.
- **Bank data never leaves the PC.** Files are read inside the browser and nothing is uploaded.
- **Scanned PDFs (photos of paper) can't be read.** Ask the bank for CSV, Excel or an electronic PDF.
- The forecast only knows what is in **Commitments**. "Add typical monthly flow" fills gaps with your 3-month average; leave it off if you enter everything yourself, or amounts are counted twice.
- Nothing is changed automatically. Scheduling and collection options are suggestions for management.

## 6. Changes made to the specification
- **Bank Charges** appeared under both Expense and Other, so it is kept once, under Expense.
- **OD Interest** is counted as an expense, because it is a real cost.
- **Returned Cheque** was added. A bounced customer cheque cancels the income it created, so income is not overstated.
- **Loans and own-account transfers** are shown separately and not counted as income or expense.
- **Duplicates:** the running balance is part of the duplicate check. Two genuine same-day, same-amount payments are therefore not wrongly removed, while re-uploading the same statement is caught.
- **Customer names:** bank descriptions rarely contain a clean customer name. "By customer" builds up as you tag customers in Needs review, because each tag becomes a rule.

## 7. Next step if several people need it
To let the Director, Finance and Accounts all see the same data from different PCs and phones, the storage layer can move to Firebase, the same approach as Mobile Distributor Pro cloud. The code is already separated for this (see the `STORAGE` section in `index.html`).
