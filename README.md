# countup-days-cash
I'm using this javascript code to count the number of days and amount of spend I've managed. You can use it for the same thing or a similar purpose by updating the days &amp; spend values as well as the text outputs. It counts up incrementally which you can also change the parameters from. 

<script>
  document.addEventListener("DOMContentLoaded", function() {
    // Calculate days since February 1, 2020
    let startDate = new Date(2020, 1, 1); // Note: JavaScript months are 0-based.
    let today = new Date();
    let timeDiff = Math.abs(today - startDate);
    let diffDays = Math.ceil(timeDiff / (1000 * 60 * 60 * 24));

    // Calculate total client media spend based on number of days
    let dailySpend = 3649.63;
    let totalSpend = diffDays * dailySpend;

    // Get the days and spend elements
    let daysElem = document.getElementById('days');
    let spendElem = document.getElementById('spend');

    // Set the initial values and the increments
    let dayValue = 0;
    let dayIncrement = 10; // Increment by 1 day at a time
    let spendValue = 0;
    let spendIncrement = totalSpend / 100; // Adjust this value to control the speed of the count-up

    // Function to update the days element
    let updateDays = () => {
        dayValue += dayIncrement;
        if (dayValue >= diffDays) {
            // Stop the interval when the target value is reached
            dayValue = diffDays; // Ensure the final value is exactly the target value
            clearInterval(daysIntervalID);
        }
        daysElem.textContent = `Over the last ${Math.round(dayValue)} Days, I've managed over`;
    };

    // Function to update the spend element
    let updateSpend = () => {
        spendValue += spendIncrement;
        if (spendValue >= totalSpend) {
            // Stop the interval when the target value is reached
            spendValue = totalSpend; // Ensure the final value is exactly the target value
            clearInterval(spendIntervalID);
        }
        spendElem.textContent = `$${spendValue.toLocaleString('en-US', {maximumFractionDigits: 2})} in client media spend.`;
    };

    // Start the count-up
    let daysIntervalID = setInterval(updateDays, 10); // Adjust the second parameter to control the speed of the count-up
    let spendIntervalID = setInterval(updateSpend, 10); // Adjust the second parameter to control the speed of the count-up
});
</script>
