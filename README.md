# wedding-countdown
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Wedding Countdown Timer</title>
    <style>
      body {
        font-family: "Times New Roman", serif; /* Elegant font */
        padding: 20px;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
        /* overflow: hidden; */
      }
      .countdown-container {
        width: 300px;
        height: auto;
        margin: 0 auto;
        background-color: #f2d7d7;
        padding: 15px;
        border-radius: 12px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        text-align: center;
        border: 2px solid #ac757e;
      }
      h1 {
        font-size: 2em;
        color: #000000; /* Hot pink color for the heading */
        margin-bottom: 10px;
      }

      /* Styling the date input field */
      input[type="date"] {
        font-family: "Times New Roman", serif; /* Custom font */
        padding: 8px;
        border: 2px solid #ac757e;
        background-color: #fffaf0;
        border-radius: 8px;
        margin-top: 5px;
        margin-bottom: 10px; /* Reduced margin to fix layout */
        width: 90%;
        font-size: 0.9em;
      }

      /* Styling the button */
      button {
        font-family: "Times New Roman", serif;
        padding: 10px 20px;
        color: #fffaf0;
        background-color: #ac757e; /* Hot pink button */
        border: none;
        border-radius: 10px;
        cursor: pointer;
        box-shadow: 2px 2px 2px black;
        font-size: 1em;
        margin-bottom: 10px;
      }

      /* Change button appearance on hover */
      button:hover {
        background-color: #fffaf0; /* Darker pink */
        color: #ac757e;
      }

      /* Styling the countdown display */
      .countdown {
        font-size: 2em;
        color: #ac757e; /* Matching pink countdown text */
        margin: 10px;
        display: none;
      }
    </style>
  </head>
  <body>
    <div class="countdown-container">
      <h1>Wedding Countdown</h1>
      <label for="date-input">Enter Your Wedding Date:</label>
      <input type="date" id="date-input" />
      <button onclick="startCountdown()">Start Countdown</button>
      <div class="countdown-result" id="countdown"></div>
    </div>
    <script>
      function startCountdown() {
        const dateInput = document.getElementById("date-input").value;
        const countdownResult = document.getElementById("countdown");

        if (!dateInput) {
          countdownResult.innerHTML = "Please enter a valid date.";
          countdownResult.style.display = "block";
          return;
        }

        const weddingDate = new Date(dateInput).setHours(0, 0, 0, 0); // Set time to midnight of wedding day
        const now = new Date().setHours(0, 0, 0, 0); // Set current time to midnight

        const updateCountdown = setInterval(function () {
          const currentTime = new Date().getTime();
          const timeDifference = weddingDate - currentTime;

          if (timeDifference === 0 || weddingDate === now) {
            clearInterval(updateCountdown);
            countdownResult.innerHTML =
              "Congratulations! 🎉 Your special day is here!";
            countdownResult.style.display = "block";
            return;
          }

          if (timeDifference < 0) {
            clearInterval(updateCountdown);
            countdownResult.innerHTML = "The wedding date has already passed!";
            countdownResult.style.display = "block";
            return;
          }

          // Time calculations for months, days, hours, minutes, and seconds
          const months = Math.floor(
            timeDifference / (1000 * 60 * 60 * 24 * 30)
          );
          const days = Math.floor(
            (timeDifference % (1000 * 60 * 60 * 24 * 30)) /
              (1000 * 60 * 60 * 24)
          );
          const hours = Math.floor(
            (timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
          );
          const minutes = Math.floor(
            (timeDifference % (1000 * 60 * 60)) / (1000 * 60)
          );
          const seconds = Math.floor((timeDifference % (1000 * 60)) / 1000);

          countdownResult.innerHTML =
            months +
            " months " +
            days +
            " days " +
            hours +
            " hours " +
            minutes +
            " minutes " +
            seconds +
            " seconds";
          countdownResult.style.display = "block";
        }, 1000); // Update the countdown every second
      }
    </script>
  </body>
</html>
