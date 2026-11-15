# PyneCore and the generated code against Pine Script, in this project

What this file is: every discrepancy found while converting and running this project's Pine
scripts, in two kinds. **Generator**: the Pyne script pine2pyne wrote from a `.pine` fails to
load or run, breaks the PyneCore specification, computes other values than the Pine source, or
a construct TradingView compiles was not converted at all. **Runtime**: PyneCore computes
something differently from Pine Script on TradingView although the generated code spells the
Pine faithfully. Every finding is one row, with the Pine construct, what happened, the fix or
workaround in force, and the basis, so that a later session, a new PyneCore release or a new
pine2pyne release can be checked against it.

Sources of truth, in this order: (1) the same script on the same bars on TradingView
("measured on TradingView", with the symbol, timeframe and date range); (2) a run of the
generated script on PyneCore (`pyne run <name>.py <data>`, the error line or the figure);
(3) the Pine Script manual. A row without a TradingView measurement goes to section 3 first.

How to update: a new generator problem is a row in section 2; a new runtime difference is a row
in section 1; something not yet measured on TradingView is a bullet in section 3 and moves to
1 or 2 once measured. Write the row when the discrepancy is found, before working around it.
Keep the minimal reproduction next to the row (`docs/probes/<id>.pine`, converted with
`pine2pyne docs/probes/<id>.pine -o docs/probes/<id>.py`, run with
`pyne run docs/probes/<id>.py demo`) when the full script is too big to read. Write the
pine2pyne and PyneCore versions and the date into the basis; when a newer version removes the
problem, say so in the row and drop the workaround instead of deleting the row. Rows that are
reported upstream carry the issue link (pine2pyne: <https://github.com/pine2pyne/pine2pyne/issues>;
PyneCore: <https://github.com/PyneSys/pynecore/issues>). A workaround in a source carries a
comment naming its row (`// pynecore_vs_pine #3` in Pine, `# pynecore_vs_pine #3` in a
hand-maintained `.py`).

Sections 1 and 2 differ: section 1 is about the **runtime** (how PyneCore executes correct Pyne
code), section 2 about the **generator** (what code pine2pyne wrote, or did not write).

---

## 1. PyneCore runtime against Pine

Each row is worked around in the Pine source (which stays the source of truth) unless marked
"no workaround yet".

| # | In Pine (TradingView) | In PyneCore | Workaround in the Pine source | Basis |
|---|-----------------------|-------------|-------------------------------|-------|
| 1 | | | | script, data, bars; TradingView measurement date; PyneCore version |

---

## 2. Generated code (pine2pyne) against Pine

Each row names the construct in the Pine source, what pine2pyne wrote in `scripts/<name>.py`
(or the message it printed instead), what happened (a message at load or run time, a failed
check of the PyneCore specification, a value that differs), and what was done: a rewrite of the
Pine that converts correctly, or a hand-maintained port.

| # | Pine construct (script, line) | What pine2pyne wrote | What happens | Fix in force | Basis |
|---|-------------------------------|----------------------|--------------|--------------|-------|
| 1 | | | | | pine2pyne version, PyneCore version, date, exact message |

---

## 3. Not measured on TradingView

- (a difference suspected from the manual or from a run, with the script and the bars to check;
  move it to section 1 or 2 once the same bars were measured on TradingView)

---

## 4. Where things are in this project

Adjust the paths to this project's layout when the file is created.

| What | Path |
|------|------|
| Pine sources (source of truth) | `scripts/<name>.pine` (PyneIDE layout) or `content/<name>.pine` (Pine-first layout); libraries `.../lib/<user>/<Name>/v<N>.pine` |
| Generated scripts and their inputs | `scripts/<name>.py`, `scripts/<name>.toml`; libraries `scripts/lib/<user>/<Name>/v<N>.py` |
| Hand-maintained ports (no longer regenerated) | `scripts/<name>.py` listed here by name, with the row that forced the port |
| Minimal reproductions of the rows above | `docs/probes/<id>.pine` and their generated `docs/probes/<id>.py` |
| Run outputs used as basis | `output/<name>.csv`, `output/<name>_strat.csv`, `output/<name>_trade.csv` |
| TradingView exports used as basis (Strategy Tester / data window CSV) | `docs/tradingview/<name>_<symbol>_<tf>_<from>_<to>.csv` |
