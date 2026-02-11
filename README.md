# Interview Practice App

A React-based interview practice application with AI-powered feedback using Claude API, Supabase authentication, and a clean dashboard interface.

## Features

- 🎯 **Mock Interviews**: Practice with 5 randomly selected behavioral questions
- 🤖 **AI Feedback**: Get scored (1-10) with 3 improvement tips per answer using Claude AI
- 📊 **Dashboard**: Track your last 10 interview sessions with scores
- 🔐 **Authentication**: Secure email/password signup and login with Supabase
- 📱 **Responsive Design**: Clean, minimal UI with Tailwind CSS

## Setup Instructions

### 1. Install Dependencies

In your terminal (make sure you're in the project directory):

```bash
npm install
```

### 2. Set Up Supabase

1. Go to [https://supabase.com](https://supabase.com) and create a free account
2. Create a new project
3. Once your project is ready, go to **Project Settings** → **API**
4. Copy your **Project URL** and **anon public key**

### 3. Create Database Table

In your Supabase project:

1. Go to **SQL Editor**
2. Run this SQL command:

```sql
CREATE TABLE interview_sessions (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  date TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  final_score DECIMAL(3,1) NOT NULL,
  questions_answered INTEGER NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE interview_sessions ENABLE ROW LEVEL SECURITY;

-- Create policy to allow users to read their own sessions
CREATE POLICY "Users can view own sessions"
  ON interview_sessions FOR SELECT
  USING (auth.uid() = user_id);

-- Create policy to allow users to insert their own sessions
CREATE POLICY "Users can insert own sessions"
  ON interview_sessions FOR INSERT
  WITH CHECK (auth.uid() = user_id);
```

### 4. Get Anthropic API Key

1. Go to [https://console.anthropic.com](https://console.anthropic.com)
2. Sign up and create an API key
3. Note: Requires payment setup, but new accounts get $5 free credits

### 5. Configure Environment Variables

1. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and add your credentials:
   ```
   VITE_SUPABASE_URL=your_supabase_project_url
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
   VITE_ANTHROPIC_API_KEY=your_anthropic_api_key
   ```

### 6. Run the App

```bash
npm run dev
```

The app will open at `http://localhost:5173`

## Deployment to Vercel

1. Install Vercel CLI:
   ```bash
   npm install -g vercel
   ```

2. Deploy:
   ```bash
   vercel
   ```

3. Add environment variables in Vercel dashboard:
   - Go to your project settings
   - Add `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, and `VITE_ANTHROPIC_API_KEY`

4. Redeploy to apply environment variables

## Usage

1. **Sign Up**: Create an account with email and password
2. **Start Interview**: Click "Start New Interview" on the dashboard
3. **Answer Questions**: You'll get 5 random behavioral questions
4. **Get Feedback**: Submit each answer to receive AI-powered scoring and tips
5. **View History**: Check your past interview sessions on the dashboard

## Tech Stack

- **Frontend**: React 18, TypeScript, Tailwind CSS
- **Build Tool**: Vite
- **Authentication & Database**: Supabase
- **AI**: Claude API (Anthropic)
- **Routing**: React Router
- **Deployment**: Vercel

## Security Note

⚠️ **Important**: This app calls the Claude API directly from the browser for simplicity. In a production environment, you should move API calls to a backend server to protect your API key.

## License

MIT
