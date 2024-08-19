- 👋 Hi, I’m @lucaspc123
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
lucaspc123/lucaspc123 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplicar Tema na Foto para Perfil</title>
    <style>
        #canvas {
            border: 1px solid black;
            border-radius: 50%;
            display: block;
            margin: auto;
        }
    </style>
</head>
<body>
    <h2 style="text-align:center;">Aplicar Tema na Foto para Perfil</h2>
    <div style="text-align: center;">
        <input type="file" id="upload" accept="image/*" />
        <br><br>
        <button id="download">Baixar Imagem</button>
        <button id="share-whatsapp">Compartilhar no WhatsApp</button>
        <button id="share-instagram">Compartilhar no Instagram</button>
        <button id="share-facebook">Compartilhar no Facebook</button>
    </div>
    <br><br>
    <canvas id="canvas" width="500" height="500"></canvas>

    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const upload = document.getElementById('upload');
        const downloadBtn = document.getElementById('download');
        const shareWhatsAppBtn = document.getElementById('share-whatsapp');
        const shareInstagramBtn = document.getElementById('share-instagram');
        const shareFacebookBtn = document.getElementById('share-facebook');

        let image = new Image();
        let themeImage = new Image();

        // Carregar o tema circular que foi processado
        themeImage.src = "circular_theme_with_transparency.png"; // Substitua isso pelo caminho correto

        upload.addEventListener('change', (e) => {
            const file = e.target.files[0];
            const reader = new FileReader();

            reader.onload = function(event) {
                image.src = event.target.result;
            };

            if (file) {
                reader.readAsDataURL(file);
            }
        });

        image.onload = function() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.save();
            ctx.beginPath();
            ctx.arc(canvas.width / 2, canvas.height / 2, canvas.width / 2, 0, Math.PI * 2, true);
            ctx.closePath();
            ctx.clip();
            ctx.drawImage(image, 0, 0, canvas.width, canvas.height);
            ctx.restore();
            applyTheme();
        };

        themeImage.onload = function() {
            applyTheme();
        };

        function applyTheme() {
            ctx.drawImage(themeImage, 0, 0, canvas.width, canvas.height); // Aplica o tema circular por cima
        }

        // Baixar Imagem
        downloadBtn.addEventListener('click', () => {
            const link = document.createElement('a');
            link.download = 'perfil-com-tema.png';
            link.href = canvas.toDataURL();
            link.click();
        });

        // Compartilhar no WhatsApp
        shareWhatsAppBtn.addEventListener('click', () => {
            const imgURL = canvas.toDataURL();
            window.open(`https://api.whatsapp.com/send?text=Confira meu novo perfil! ${imgURL}`, '_blank');
        });

        // Compartilhar no Instagram (por enquanto não existe API direta para isso, então você pode sugerir baixar e enviar manualmente)
        shareInstagramBtn.addEventListener('click', () => {
            alert("Baixe a imagem e poste manualmente no Instagram.");
        });

        // Compartilhar no Facebook
        shareFacebookBtn.addEventListener('click', () => {
            const imgURL = canvas.toDataURL();
            const shareUrl = `https://www.facebook.com/sharer/sharer.php?u=${encodeURIComponent(imgURL)}`;
            window.open(shareUrl, 'facebook-share-dialog', 'width=800,height=600');
        });
    </script>
</body>
</html>
