# Web Scraping + MongoDB Quote Management System

A complete data pipeline that scrapes quotes from the web, stores them in MongoDB, and provides search functionality with message queue processing for notifications.

## What This Project Simulates

This project simulates a content aggregation service that collects inspirational quotes from websites and makes them available through a searchable database. It combines:

- Web scraping to automatically collect quotes and author information
- Data storage in a NoSQL database for flexible content management  
- Search functionality to find quotes by various criteria
- Background processing for user notifications when new content is added

This represents a real-world data pipeline used by content platforms, news aggregators, or quote/inspiration apps.

## Features

- Web scraping using BeautifulSoup to extract quotes and author data
- MongoDB integration with MongoEngine ODM for data persistence
- RabbitMQ message queuing for asynchronous user notification processing
- Interactive search interface for finding quotes by author, tag, or multiple tags
- Data export functionality to JSON format
- Producer/Consumer pattern for scalable notification system

## Technologies Used

- Web Scraping: BeautifulSoup4 and Requests
- Database: MongoDB with MongoEngine ODM
- Message Broker: RabbitMQ with Pika library
- Data Processing: Python with JSON handling
- Test Data Generation: Faker for user simulation
- Configuration: ConfigParser for credential management

## Prerequisites

- Python 3.7+
- MongoDB Atlas account or local MongoDB instance
- RabbitMQ server
- Internet connection for web scraping

## Installation

1. Clone the repository
   ```bash
   git clone <repository-url>
   cd Scrapy+Mongo_DB
   ```

2. Install dependencies
   ```bash
   pip install requests beautifulsoup4 mongoengine pika faker configparser
   ```

3. Configure database connection
   
   Copy the example config and add your credentials:
   ```bash
   cp configs/config.ini.example configs/config.ini
   ```
   
   Edit `configs/config.ini` with your MongoDB credentials:
   ```ini
   [DB]
   USER=your_mongodb_username
   PASS=your_mongodb_password
   DOMAIN=your_mongodb_cluster.mongodb.net
   ```

4. Start RabbitMQ server
   ```bash
   # Using Docker
   docker run -d --hostname rabbitmq --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
   ```

## Usage

### 1. Scrape Data from Web
```bash
python main.py
```
This will:
- Scrape quotes from https://quotes.toscrape.com/
- Extract author biographical information
- Save data to JSON files in `contents/` folder
- Handle duplicate authors automatically

### 2. Import Data to MongoDB
```bash
python seeds.py
```
This will:
- Clear existing database data
- Import authors from `contents/authors.json`
- Import quotes from `contents/quotes.json`
- Create relationships between quotes and authors

### 3. Search Through Quotes
```bash
python request.py
```

Commands:
- `name:Albert Einstein` - Find quotes by author name
- `tag:life` - Find quotes by single tag
- `tags:life,wisdom,success` - Find quotes by multiple tags
- `exit` - Exit the application

### 4. Run Notification System
Generate users and queue notifications:
```bash
python producer.py
```

Process notification queue:
```bash
python consumer.py
```

## Key Features

### Web Scraping Pipeline
- Automated data extraction from multiple website pages
- Author profile scraping with detailed biographical information
- Duplicate detection and removal
- Error handling for network requests

### MongoDB Operations
- Document modeling with relationships between quotes and authors
- Efficient querying with tag-based search
- Data validation and type checking
- Connection management with authentication

### Message Queue Processing
- Producer pattern for generating user notifications
- Consumer pattern for processing email notifications
- Message persistence and acknowledgment
- Scalable background processing

### Search Functionality
- Interactive command-line interface
- Multiple search criteria (author, tags, multiple tags)
- Real-time query processing
- User-friendly result display

## Data Flow

1. **Web Scraping**: Extract quotes and authors from target website
2. **Data Processing**: Clean and structure scraped data into JSON format
3. **Database Import**: Store processed data in MongoDB with proper relationships
4. **Search Interface**: Allow users to query the database interactively
5. **Notification System**: Queue and process user notifications for new content

## Sample Data

The system scrapes and stores:
- **Quotes**: Inspirational quotes with associated tags and author references
- **Authors**: Detailed biographical information including birth dates, locations, and descriptions
- **Users**: Generated test users for notification system testing

## Development Features

- Modular code structure separating scraping, storage, and processing
- Configuration-based database connection management
- JSON data format for easy inspection and debugging
- Comprehensive error handling and logging
- Extensible search functionality

## Workflow

1. **Data Collection**: Run web scraper to gather fresh quote content
2. **Data Storage**: Import scraped data into MongoDB database
3. **Content Search**: Use interactive interface to explore quote database
4. **User Management**: Generate test users and process notifications
5. **Background Processing**: Handle user notifications asynchronously