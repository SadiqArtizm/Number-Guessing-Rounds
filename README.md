import inquirer from "inquirer";

const totalRounds = 3;
let roundsPlayed = 0;

interface Answers {
    userGuess: string;
}

async function playRound(): Promise<void> {
    const sysTemGeneratedNum = Math.floor(Math.random() * 10);

    const answers: Answers = await inquirer.prompt([
        {
            type: "input",
            name: "userGuess",
            message: "Write Your Guess b/w 1 to 10:",
            validate: (input: string) => {
                const isValid = !isNaN(Number(input)) && Number(input) >= 1 && Number(input) <= 10;
                return isValid || "Please enter a number between 1 and 10.";
            },
        },
    ]);

    const { userGuess } = answers;
    console.log(userGuess, "userGuess", sysTemGeneratedNum, "System");

    if (parseInt(userGuess, 10) === sysTemGeneratedNum) {
        console.log("Yeaaa Your answer is correct \n You Win");
    } else {
        console.log("Please Try Again Better Luck Next Time");
    }
}

async function main(): Promise<void> {
    while (roundsPlayed < totalRounds) {
        await playRound();
        roundsPlayed++;
    }

    console.log(`Game Over! You played ${totalRounds} rounds.`);
}

main();
