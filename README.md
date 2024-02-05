# GiftExchange2
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>プレゼント交換</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }

        h1 {
            color: #4285f4;
        }

        #result {
            margin-top: 20px;
            font-weight: bold;
            color: #34a853;
        }
    </style>
</head>
<body>

    <h1>プレゼント交換</h1>

    <form id="participantsForm">
        <label for="participantNames">参加者の名前（コンマで区切って入力）：</label>
        <input type="text" id="participantNames" required>
        <button type="button" onclick="assignGift()">プレゼントを交換する</button>
    </form>

    <div id="result"></div>

    <script>
        function assignGift() {
            const participantNamesInput = document.getElementById("participantNames");
            const participantNames = participantNamesInput.value.split(",").map(name => name.trim());

            if (participantNames.length < 2) {
                alert("少なくとも2人以上の参加者が必要です。");
                return;
            }

            const shuffledNames = shuffle(participantNames.slice());
            const resultMessage = generateResultMessage(participantNames, shuffledNames);

            document.getElementById("result").innerText = resultMessage;
        }

        function shuffle(array) {
            let currentIndex = array.length, randomIndex;

            while (currentIndex !== 0) {
                randomIndex = Math.floor(Math.random() * currentIndex);
                currentIndex--;

                [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
            }

            return array;
        }

        function generateResultMessage(originalNames, shuffledNames) {
            let resultMessage = "プレゼントの交換結果:\n\n";

            for (let i = 0; i < originalNames.length; i++) {
                resultMessage += `${originalNames[i]} さん → ${shuffledNames[i]} さん\n`;
            }

            return resultMessage;
        }
    </script>

</body>
</html>
