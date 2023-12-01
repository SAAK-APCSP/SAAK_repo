# Ascii Binary project

<script>
const BITS_IN_BYTE = 8; // Constant for bits in a byte
function printBulb(bit) {
    if (bit === 0) {
        // Dark emoji
        console.log(":black_circle:");
    } else if (bit === 1) {
        // Light emoji
        console.log(":large_yellow_circle:");
    }
}
function main() {
    const message = prompt("Enter a message:"); // Prompt for message
    for (let i = 0; i < message.length; i++) {
        const decimal = message.charCodeAt(i); // Get ASCII version of parsed character
        if (decimal === 0) {
            printBulb(0); // Input 0 into printBulb function
        } else if (decimal !== 0) {
            const bits = new Array(BITS_IN_BYTE).fill(0);
            for (let j = BITS_IN_BYTE - 1; j >= 0; j--) {
                bits[j] = decimal % 2; // Position in array is remainder of decimal version of ASCII (1 or 0)
                decimal = Math.floor(decimal / 2); // Decimal is changed to the floor of the decimal / 2
            }
            bits.forEach((bit) => {
                printBulb(bit); // Print bulb for every bit
            });
            console.log(); // Print new line for a new set of 8 bulbs
        }
    }
}
main();
</script>









