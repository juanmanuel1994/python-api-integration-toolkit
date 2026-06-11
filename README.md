# Support Ticket System

A lightweight web application built with **Flask** and **SQLite** for managing support tickets. Features a live dashboard with metrics, agent management, priority/status workflows, and one-click CSV/XLSX export.

## Features

| Feature | Details |
|---|---|
| Ticket management | Create, view, edit, delete tickets |
| Statuses | `open` → `in-progress` → `closed` |
| Priorities | `low`, `medium`, `high`, `critical` |
| Agent assignment | Assign/reassign tickets to support agents |
| Dashboard | Tickets by status, priority breakdown, avg. resolution time, top agent |
| Search & filter | Filter by status, priority, or free-text search |
| Export | Download all tickets as CSV or XLSX (via pandas) |
| UI | Responsive Bootstrap 5 with sidebar navigation |

## Requirements

- Python 3.8+
- pip packages: `flask`, `pandas`, `openpyxl`

## Installation

```bash
# 1. Navigate to the project folder
cd support_tickets

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate      # Linux/macOS
venv\Scripts\activate         # Windows

# 3. Install dependencies
pip install flask pandas openpyxl

# 4. Run the application
python app.py
```

Then open [http://127.0.0.1:5000](http://127.0.0.1:5000) in your browser.

The SQLite database (`tickets.db`) is created automatically on first run.

## Project Structure

```
support_tickets/
├── app.py               # Flask app, routes, DB helpers
├── tickets.db           # SQLite database (auto-created)
├── README.md
└── templates/
    ├── base.html        # Shared layout (sidebar, nav)
    ├── dashboard.html   # Metrics dashboard
    ├── tickets.html     # Ticket list with filters
    ├── ticket_detail.html  # Single ticket view + actions
    ├── ticket_form.html    # Create/edit form
    ├── agents.html      # Agent list
    └── agent_form.html  # Add agent form
```

## Usage

### Creating a ticket
1. Click **New Ticket** from the sidebar or dashboard.
2. Fill in the title, description, priority, and optionally assign an agent.
3. Submit — ticket appears in the list with status `open`.

### Updating status
- Open a ticket → use the **Update Status** panel on the right.
- Or click **Edit** to change all fields at once.
- Closing a ticket automatically records the `closed_at` timestamp used for avg. resolution time.

### Assigning tickets
- Open a ticket → use the **Assign Agent** panel.
- Agents are managed under the **Agents** section in the sidebar.

### Exporting data
- Click **Export CSV** or **Export XLSX** in the sidebar to download all tickets.
- The file includes: id, title, description, status, priority, agent, created_at, updated_at, closed_at.

## Dashboard Metrics

| Metric | Description |
|---|---|
| Open / In Progress / Closed | Count of tickets per status |
| Avg. Resolution Time | Mean hours from `created_at` to `closed_at` |
| Top Performer | Agent with the most closed tickets |
| Priority Breakdown | Bar chart of ticket counts per priority level |

## Configuration

The secret key is set in `app.py` (`app.secret_key`). Change it before deploying to production:

```python
app.secret_key = "your-secure-random-key"
```
