// Dados de exemplo (substitua pelos seus filmes/séries)
const filmes = [
    { titulo: "Duna 2", imagem: "https://via.placeholder.com/200x300/333?text=Duna+2" },
    { titulo: "Oppenheimer", imagem: "https://via.placeholder.com/200x300/333?text=Oppenheimer" },
    { titulo: "Batman", imagem: "https://via.placeholder.com/200x300/333?text=Batman" },
    { titulo: "Avatar 2", imagem: "https://via.placeholder.com/200x300/333?text=Avatar+2" },
    { titulo: "Top Gun", imagem: "https://via.placeholder.com/200x300/333?text=Top+Gun" },
];

const series = [
    { titulo: "Stranger Things", imagem: "https://via.placeholder.com/200x300/555?text=Stranger+Things" },
    { titulo: "The Last of Us", imagem: "https://via.placeholder.com/200x300/555?text=The+Last+of+Us" },
    { titulo: "Breaking Bad", imagem: "https://via.placeholder.com/200x300/555?text=Breaking+Bad" },
    { titulo: "Game of Thrones", imagem: "https://via.placeholder.com/200x300/555?text=Game+of+Thrones" },
];

// Função para criar os itens do carrossel
function criarCarrossel(dados, classe) {
    const container = document.querySelector(`.${classe}`);
    container.innerHTML = dados.map(item => `
        <div class="item">
            <img src="${item.imagem}" alt="${item.titulo}">
            <div class="item-info">
                <h3>${item.titulo}</h3>
            </div>
        </div>
    `).join('');
}

// Inicializa os carrosséis
criarCarrossel(filmes, "filmes");
criarCarrossel(series, "series");

// Navegação dos botões
document.querySelectorAll('.carrossel').forEach(carrossel => {
    const btnPrev = carrossel.querySelector('.prev');
    const btnNext = carrossel.querySelector('.next');
    const container = carrossel.querySelector('div:not(.btn)');
    let scrollPos = 0;

    btnNext.addEventListener('click', () => {
        scrollPos += 220; // Largura do item + gap
        if (scrollPos > container.scrollWidth - container.clientWidth) {
            scrollPos = 0;
        }
        container.scrollTo({ left: scrollPos, behavior: 'smooth' });
    });

    btnPrev.addEventListener('click', () => {
        scrollPos -= 220;
        if (scrollPos < 0) {
            scrollPos = container.scrollWidth;
        }
        container.scrollTo({ left: scrollPos, behavior: 'smooth' });
    });
});
