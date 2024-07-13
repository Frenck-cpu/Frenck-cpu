#!/bin/bash

# Informações do usuário
GITHUB_USER="Frenck-cpu"
REPO_NAME="Frenck-ednilton-LP"
BRANCH_NAME="main"  # ou "master"

# Clonar o repositório
git clone https://github.com/$GITHUB_USER/$REPO_NAME.git
cd $REPO_NAME

# Estrutura do projeto
mkdir css js images
echo "<!DOCTYPE html>
<html lang=\"en\">
<head>
    <meta charset=\"UTF-8\">
    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">
    <title>Frenck's Store</title>
    <link rel=\"stylesheet\" href=\"css/styles.css\">
</head>
<body>
    <header>
        <h1>Welcome to Frenck's Store</h1>
    </header>
    <main>
        <section id=\"intro\">
            <h2>Discover Our Products</h2>
            <p>We offer a range of infoproducts and physical products to meet your needs.</p>
        </section>
        <section id=\"products\">
            <h2>Our Products</h2>
            <div class=\"product\">
                <h3>Product 1</h3>
                <img src=\"images/product1.jpg\" alt=\"Product 1\">
                <p>Short description of Product 1.</p>
                <button>Buy Now</button>
            </div>
            <div class=\"product\">
                <h3>Product 2</h3>
                <img src=\"images/product2.jpg\" alt=\"Product 2\">
                <p>Short description of Product 2.</p>
                <button>Buy Now</button>
            </div>
            <!-- Add more products as needed -->
        </section>
        <section id=\"contact\">
            <h2>Contact Us</h2>
            <form>
                <label for=\"name\">Name:</label>
                <input type=\"text\" id=\"name\" name=\"name\" required>
                <label for=\"email\">Email:</label>
                <input type=\"email\" id=\"email\" name=\"email\" required>
                <label for=\"message\">Message:</label>
                <textarea id=\"message\" name=\"message\" required></textarea>
                <button type=\"submit\">Send</button>
            </form>
        </section>
    </main>
    <footer>
        <p>&copy; 2024 Frenck's Store. All rights reserved.</p>
    </footer>
    <script src=\"js/scripts.js\"></script>
</body>
</html>" > index.html

echo "body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
header { background-color: #4CAF50; color: white; padding: 1em 0; text-align: center; }
main { padding: 1em; }
section { margin-bottom: 2em; }
.product { border: 1px solid #ddd; padding: 1em; margin-bottom: 1em; }
.product img { max-width: 100%; height: auto; }
form { display: flex; flex-direction: column; }
form label { margin-bottom: 0.5em; }
form input, form textarea { margin-bottom: 1em; padding: 0.5em; border: 1px solid #ddd; }
form button { padding: 0.5em; background-color: #4CAF50; color: white; border: none; cursor: pointer; }
form button:hover { background-color: #45a049; }
footer { background-color: #f1f1f1; text-align: center; padding: 1em 0; margin-top: 2em; }" > css/styles.css

echo "document.addEventListener('DOMContentLoaded', function() {
    console.log('Page loaded successfully!');
    // Add any JavaScript needed for your landing page
});" > js/scripts.js

# Adicionar arquivos ao repositório
git add .
git commit -m "Initial commit with landing page structure"

# Fazer push para o GitHub
git push -u origin $BRANCH_NAME

# Configurar o GitHub Pages
curl -X POST -H "Accept: application/vnd.github.v3+json" \
    https://api.github.com/repos/$GITHUB_USER/$REPO_NAME/pages \
    -d '{"source":{"branch":"'$BRANCH_NAME'","path":"/"}}'

echo "Landing page configurada com sucesso! Acesse em: https://$GITHUB_USER.github.io/$REPO_NAME/"
