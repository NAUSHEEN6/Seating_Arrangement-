# Seating_Arrangement
<script>
    const employees = [
        { name: "Alice" }, { name: "Bob" }, /* up to 33 employees */
    ];

    function bookAllSeats() {
        let tempEmployees = employees.slice(0, 25);
        let remainingEmployees = employees.slice(25, 33);

        const seatNumbers = [
            23, 24, 25, 26,
            27, 28, 29,
            30, 31, 32, 33, 34, 35, 36, 37,
            38, 39, 40, 41, 42, 43,
            44, 45, 46, 47
        ];

        let bookedSeats = tempEmployees.reduce((acc, em, index) => {
            let seatKey = 'Seat-' + seatNumbers[index];
            acc[seatKey] = em?.name || 'Unknown';
            return acc;
        }, {});

        const today = new Date().toISOString().split('T')[0];
        localStorage.setItem(`bookedSeats_${today}`, JSON.stringify(bookedSeats));

        console.log("Booked seats saved for:", today);
        console.log(bookedSeats);
        console.log("Remaining employees:", remainingEmployees);
    }

    // Auto-run on page load
    window.onload = function() {
        const today = new Date().toISOString().split('T')[0];
        const alreadyBooked = localStorage.getItem(`bookedSeats_${today}`);

        if (!alreadyBooked) {
            console.log("Auto-booking seats for today:", today);
            bookAllSeats();
        } else {
            console.log("Seats already booked for today:", today);
        }
    };
</script>
