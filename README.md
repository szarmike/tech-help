<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Service Order Form</title>

  <!-- Flatpickr styles -->
  <link 
    rel="stylesheet" 
    href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css"
  >

  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
    }
    body {
      font-family: sans-serif;
      font-size: 27px;
      display: flex;
      justify-content: center;
      align-items: center;
      background: #f9f9f9;
    }
    form {
      width: 90%;
      max-width: 500px;
      padding: 1em;
      background: white;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      box-sizing: border-box;
      border-radius: 8px;
    }
    label {
      display: block;
      margin-bottom: 1em;
    }
    input, select, textarea, .flatpickr-input {
      width: 100%;
      padding: 0.5em;
      font-size: 1em;
      box-sizing: border-box;
    }
    button {
      padding: 0.75em 1.5em;
      cursor: pointer;
      font-size: 1em;
    }
    .flatpickr-day.disabled {
      background: #eee;
      color: #999;
      cursor: not-allowed;
    }
    .legend {
      font-size: 0.8em;
      color: #555;
      margin-bottom: 1em;
    }
  </style>
</head>
<body>
  <form
    action="https://formspree.io/f/mwpoyyzo"
    method="POST"
  >
    <h2>Place Your Order</h2>

    <!-- Name -->
    <label for="name">
      Your Name:
      <input
        type="text"
        id="name"
        name="name"
        placeholder="Jane Doe"
        required
      >
    </label>

    <!-- Email -->
    <label for="email">
      Your Email:
      <input
        type="email"
        id="email"
        name="_replyto"
        placeholder="jane@example.com"
        required
      >
    </label>

    <!-- Address -->
    <label for="address">
      Address:
      <textarea
        id="address"
        name="address"
        rows="3"
        placeholder="Street address, city, state, ZIP"
        required
      ></textarea>
    </label>

    <!-- PC Type -->
    <label for="pc">
      PC Type:
      <select id="pc" name="pc" required>
        <option value="">-- Select PC Type --</option>
        <option value="none">None</option>
        <option value="desktop">Desktop PC</option>
        <option value="laptop">Laptop PC</option>
        <option value="workstation">Workstation PC</option>
        <option value="mini">Mini PC</option>
      </select>
    </label>

    <!-- Service -->
    <label for="service">
      Service:
      <select id="service" name="service" required>
        <option value="">-- Select a Service --</option>
        <option value="1-screen">1 Screen</option>
        <option value="2-screen">2 Screen</option>
        <option value="3-screen">3 Screen</option>
        <option value="mouse-keyboard">Mouse + Keyboard</option>
        <option value="making-pc-account">Making PC Account</option>
        <option value="troubleshoot">Troubleshoot</option>
        <option value="setup">Setup</option>
      </select>
    </label>

    <!-- Legend for blocked dates -->
    <div class="legend">
      Unavailable dates: <br>
      – Weekdays (Mon–Fri) from Aug 10 to May 30 <br>
      – All days from June 7 to July 4
    </div>

    <!-- Installation Dates -->
    <label for="installDates">
      Installation Date(s):
      <input
        type="text"
        id="installDates"
        name="installDates"
        placeholder="Select install dates"
        readonly
        required
        class="flatpickr-input"
      >
    </label>

    <!-- Email handling (Formspree) -->
    <input type="hidden" name="_to" value="ms2man24@gmail.com">
    <input type="hidden" name="_subject" value="🌟 New Order Received">
    <input type="hidden" name="_next" value="https://yourdomain.com/thank-you.html">

    <button type="submit">Submit Order</button>
  </form>

  <!-- Flatpickr script -->
  <script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>
  <script>
    flatpickr("#installDates", {
      mode: "multiple",
      dateFormat: "Y-m-d",
      disable: [
        // Block all weekdays (Mon–Fri) between Aug 10 → May 30
        function(date) {
          const m = date.getMonth() + 1, d = date.getDate();
          const day = date.getDay();
          const inSchoolRange =
            (m > 8 || (m === 8 && d >= 10)) ||
            (m < 6 || (m === 5 && d <= 30));
          return inSchoolRange && (day >= 1 && day <= 5);
        },
        // Block every date from June 7 → July 4
        {
          from: new Date(new Date().getFullYear(), 5, 7),
          to:   new Date(new Date().getFullYear(), 6, 4)
        }
      ],
      locale: { firstDayOfWeek: 1 }
    });
  </script>
</body>
</html>
