# 🎮 Dota2 Companion

A full-stack Dota2 companion application that provides heroes, teams, and match information through a modern web interface. Built with microservices architecture using Docker Compose.

## 🏗️ Architecture

This project consists of three main services:

- **Frontend** (`dota2-vue-app`): Vue.js application with Tailwind CSS
- **Backend API** (`dota2-api-backend`): Node.js/Express/TypeScript API
- **Redis**: Caching and data storage

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Vue.js App    │───▶│  Express API    │───▶│  OpenDota API   │
│   (Port 8080)   │    │  (Port 3000)    │    │   (External)    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │
                                ▼
                       ┌─────────────────┐
                       │     Redis       │
                       │   (Port 6379)   │
                       └─────────────────┘
```

## 🚀 Quick Start

### Prerequisites
- Docker and Docker Compose
- Git

### Running the Application

1. **Clone the repository with submodules:**
   ```bash
   git clone --recurse-submodules https://github.com/your-username/dota2-companion.git
   cd dota2-companion
   ```

2. **If you already cloned without submodules:**
   ```bash
   git submodule update --init --recursive
   ```

3. **Start all services:**
   ```bash
   docker-compose up --build
   ```

4. **Access the application:**
   - Frontend: http://localhost:8080
   - Backend API: http://localhost:3000
   - Redis: localhost:6379

## 🔧 Environment Configuration

The application uses the following environment variables (configured in docker-compose.yml):

### Backend Environment Variables
- `PORT`: Server port (default: 3000)
- `DOTA_SITE`: Frontend URL for CORS (default: http://localhost:8080)
- `OPEN_DOTA_API_URL`: OpenDota API endpoint (default: https://api.opendota.com/api)
- `REDIS_STRING_URL`: Redis connection string (default: redis://redis:6379)

### Frontend Environment Variables
- `VUE_APP_DOTA_BACKEND_API`: Backend API URL (default: http://api:3000)

## 📁 Project Structure

```
dota2-companion/
├── docker-compose.yml          # Service orchestration
├── .gitmodules                 # Git submodule configuration
├── README.md                   # This file
├── dota2-api-backend/          # Backend API (submodule)
│   ├── src/                    # TypeScript source code
│   ├── Dockerfile              # Backend container configuration
│   ├── package.json            # Backend dependencies
│   └── README.md               # Backend documentation
└── dota2-vue-app/              # Frontend application (submodule)
    ├── src/                    # Vue.js source code
    ├── public/                 # Static assets
    ├── Dockerfile              # Frontend container configuration
    ├── package.json            # Frontend dependencies
    └── README.md               # Frontend documentation
```

## 🛠️ Development

### Individual Service Development

#### Backend Development
```bash
cd dota2-api-backend
npm install
npm run dev
```

#### Frontend Development
```bash
cd dota2-vue-app
npm install
npm run serve
```

### Adding New Features

1. **Backend Changes**: Modify code in `dota2-api-backend/src/`
2. **Frontend Changes**: Modify code in `dota2-vue-app/src/`
3. **Test with Docker**: `docker-compose up --build`

## 📦 Services Details

### Backend API (`dota2-api-backend`)
- **Framework**: Express.js with TypeScript
- **Features**: 
  - Fetches data from OpenDota API
  - Redis caching for performance
  - CORS configuration for frontend
- **Port**: 3000
- **Health Check**: Available at `/health`

### Frontend (`dota2-vue-app`)
- **Framework**: Vue.js 2
- **Styling**: Tailwind CSS
- **Features**:
  - Heroes information display
  - Team and matchup analysis
  - Responsive design
- **Port**: 8080

### Redis
- **Purpose**: Caching API responses
- **Port**: 6379
- **Database**: Default database (0)

## 🔍 API Endpoints

The backend provides endpoints for:
- Hero information and statistics
- Team data and matchups
- Match history and analysis
- Cached responses for better performance

## 🐛 Troubleshooting

### Common Issues

1. **Submodules appear empty**:
   ```bash
   git submodule update --init --recursive
   ```

2. **Port conflicts**:
   - Check if ports 3000, 6379, or 8080 are in use
   - Modify ports in `docker-compose.yml` if needed

3. **Build failures**:
   ```bash
   docker-compose down
   docker-compose up --build --force-recreate
   ```

4. **Environment variables not working**:
   - Check the Docker Compose environment configuration
   - Verify `.env` files in submodules if used locally

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes in the appropriate submodule
4. Test with Docker Compose
5. Commit your changes: `git commit -m 'Add feature'`
6. Push to the branch: `git push origin feature-name`
7. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [OpenDota API](https://docs.opendota.com/) for providing Dota2 data
- [Vue.js](https://vuejs.org/) for the frontend framework
- [Express.js](https://expressjs.com/) for the backend framework
- [Tailwind CSS](https://tailwindcss.com/) for styling

## 🔗 Related Repositories

- [Backend API](https://github.com/johnmichealacera/dota2-api-backend)
- [Frontend App](https://github.com/johnmichealacera/dota2-vue-app)

---

**Happy coding and may your MMR rise! 🎮**
