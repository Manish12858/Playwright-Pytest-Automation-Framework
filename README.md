# Playwright + Pytest Automation Framework

UI and API test automation in **Python** using **Playwright** and **Pytest**.
I built this while learning test automation, step by step from pytest basics to a small framework with Page Object Model, API + UI end-to-end tests, network mocking, data-driven tests and BDD.

Tests run against the public practice apps on [rahulshettyacademy.com](https://rahulshettyacademy.com) (e-commerce client app, login page practice and automation practice pages).

## Tech stack

- Python 3.12
- Playwright (sync API) with `pytest-playwright`
- Pytest: fixtures, markers, parametrize, custom command line options
- `pytest-bdd` for Gherkin feature files
- `pytest-xdist` for parallel runs, `pytest-html` for HTML reports

## What is covered

| Area | File |
|---|---|
| Pytest fixtures (`scope`, `yield` teardown), `conftest.py`, `smoke` / `skip` markers | `pytestDir/` |
| Browser, context and page, core locators (`get_by_label`, `get_by_role`, `get_by_text`), Chromium and Firefox | `test_playwrightBasics.py` |
| Dynamic cart validation, child window / popup handling | `test_UIValidations_1.py` |
| Hidden elements, alert dialogs, mouse hover, iframes, web table lookup | `test_MoreValidations.py` |
| Create order through API, then verify it in the UI | `test_web_api.py`, `utils/apiBase.py` |
| Network interception: mock API response, change request URL, login with token in local storage | `test_Network1.py`, `test_Network2.py` |
| Framework test: Page Object Model + API utils + JSON test data + parametrize | `test_framework_web_api.py`, `pageObjects/`, `utils/apiBaseFramework.py`, `data/credentials.json` |
| BDD scenario outline for the order flow | `features/orderTransaction.feature`, `test_pytest-bddTest.py` |

## Project structure

```
├── pytestDir/                    # pytest basics (fixtures, conftest, markers)
│   ├── conftest.py
│   ├── test_PyTestValidation.py
│   └── test_2PyTestValidation.py
├── playwright/
│   ├── conftest.py               # --browser_name / --url_name options, browserInstance fixture
│   ├── data/credentials.json     # test users for data-driven run
│   ├── features/                 # BDD feature files
│   ├── pageObjects/              # login, dashboard, orders history, order details pages
│   ├── utils/                    # API helpers (login token, create order)
│   └── test_*.py
├── pytest.ini
└── requirements.txt
```

## Setup

```bash
git clone https://github.com/Manish12858/Playwright-Pytest-Automation-Framework.git
cd Playwright-Pytest-Automation-Framework
pip install -r requirements.txt
playwright install
```

**Login details:** the email and password in the code (`testuser@example.com` / `Test@1234`) are dummy values. Register your own account on https://rahulshettyacademy.com/client and put it in `playwright/data/credentials.json`, `features/orderTransaction.feature`, `utils/apiBase.py` and the network / web api tests before running them.

## Running tests

Run the Playwright tests from inside the `playwright` folder (the JSON data file is read with a relative path):

```bash
cd playwright

# all tests in headed mode
pytest --headed

# only smoke tests, on chrome, 3 in parallel, with trace and HTML report
pytest --browser_name chrome -m smoke -n 3 --tracing on --html=report.html

# run on firefox
pytest test_framework_web_api.py --browser_name firefox

# BDD scenario
pytest test_pytest-bddTest.py
```

Pytest basics:

```bash
cd pytestDir
pytest -v -s
```

`report.html` and the trace files are generated on each run, so they are not committed.
