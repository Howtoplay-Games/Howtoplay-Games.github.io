import React, { useState, useEffect } from 'react';
import { ExternalLink, Code, Users, Trophy, Github, Mail, MessageSquare } from 'lucide-react';

// LOAD CONFIGURATION FROM config.json
// In a real setup, you would fetch this from a config.json file
// For this demo, paste your config.json content below

const CONFIG = {
  "personal": {
    "name": "Your Name",
    "title": "Roblox Game Developer",
    "avatar": "https://tr.rbxcdn.com/30DAY-AvatarHeadshot-B8D6A1F0E5024AE0A7C8D9E4E5B8F9A1-Png/150/150/AvatarHeadshot/Png/noFilter",
    "bio": "Passionate Roblox developer specializing in engaging gameplay mechanics and immersive experiences. Over X years of experience creating successful games with millions of visits.",
    "robloxProfile": "https://www.roblox.com/users/YOUR_USER_ID/profile"
  },
  
  "games": [
    {
      "title": "Game Title 1",
      "description": "An exciting adventure game with unique mechanics and engaging storyline.",
      "image": "https://images.unsplash.com/photo-1511512578047-dfb367046420?w=500&h=300&fit=crop",
      "link": "https://www.roblox.com/games/GAME_ID_1",
      "visits": "10M+",
      "rating": "95%",
      "featured": true
    },
    {
      "title": "Game Title 2",
      "description": "Fast-paced multiplayer combat experience with advanced mechanics.",
      "image": "https://images.unsplash.com/photo-1538481199705-c710c4e965fc?w=500&h=300&fit=crop",
      "link": "https://www.roblox.com/games/GAME_ID_2",
      "visits": "5M+",
      "rating": "92%",
      "featured": true
    },
    {
      "title": "Game Title 3",
      "description": "Creative building simulator with social features.",
      "image": "https://images.unsplash.com/photo-1552820728-8b83bb6b773f?w=500&h=300&fit=crop",
      "link": "https://www.roblox.com/games/GAME_ID_3",
      "visits": "2M+",
      "rating": "90%",
      "featured": false
    },
    {
      "title": "Game Title 4",
      "description": "RPG adventure with custom quest system.",
      "image": "https://images.unsplash.com/photo-1542751371-adc38448a05e?w=500&h=300&fit=crop",
      "link": "https://www.roblox.com/games/GAME_ID_4",
      "visits": "1M+",
      "rating": "88%",
      "featured": false
    }
  ],
  
  "skills": [
    { "name": "Lua Scripting", "level": 95 },
    { "name": "Game Design", "level": 90 },
    { "name": "UI/UX Design", "level": 85 },
    { "name": "3D Modeling", "level": 75 },
    { "name": "Animation", "level": 80 },
    { "name": "VFX & Particles", "level": 85 }
  ],
  
  "stats": [
    { "icon": "Users", "label": "Total Visits", "value": "20M+" },
    { "icon": "Trophy", "label": "Games Published", "value": "15+" },
    { "icon": "Code", "label": "Years Experience", "value": "5+" },
    { "icon": "Users", "label": "Active Players", "value": "50K+" }
  ],
  
  "contact": {
    "email": "your.email@example.com",
    "discord": "YourDiscord#0000",
    "github": "https://github.com/yourusername",
    "twitter": "https://twitter.com/yourusername"
  },
  
  "theme": {
    "primary": "#3b82f6",
    "secondary": "#8b5cf6",
    "accent": "#ec4899"
  }
};

// Icon mapping for stats
const iconMap = {
  Users: Users,
  Trophy: Trophy,
  Code: Code
};

export default function RobloxPortfolio() {
  const [activeSection, setActiveSection] = useState('home');
  const [scrolled, setScrolled] = useState(false);

  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > 50);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const featuredGames = CONFIG.games.filter(g => g.featured);

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 text-white">
      {/* Configuration Notice */}
      <div className="bg-blue-600 text-white py-2 px-4 text-center text-sm">
        📝 <strong>Setup Required:</strong> Edit the CONFIG object at the top of this file or use config.json. See README for instructions.
      </div>

      {/* Navigation */}
      <nav className={`fixed top-10 w-full z-50 transition-all duration-300 ${scrolled ? 'bg-slate-900/95 backdrop-blur-md shadow-lg' : 'bg-transparent'}`}>
        <div className="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
          <div className="text-2xl font-bold bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent">
            {CONFIG.personal.name}
          </div>
          <div className="flex gap-6">
            {['Home', 'Games', 'Skills', 'Contact'].map(section => (
              <button
                key={section}
                onClick={() => {
                  setActiveSection(section.toLowerCase());
                  document.getElementById(section.toLowerCase())?.scrollIntoView({ behavior: 'smooth' });
                }}
                className="hover:text-blue-400 transition-colors"
              >
                {section}
              </button>
            ))}
          </div>
        </div>
      </nav>

      {/* Hero Section */}
      <section id="home" className="min-h-screen flex items-center justify-center px-6 pt-20">
        <div className="max-w-6xl w-full grid md:grid-cols-2 gap-12 items-center">
          <div className="space-y-6">
            <div className="inline-block px-4 py-2 bg-blue-500/20 rounded-full text-blue-300 text-sm font-semibold">
              {CONFIG.personal.title}
            </div>
            <h1 className="text-6xl font-bold leading-tight">
              Hi, I'm <span className="bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent">
                {CONFIG.personal.name}
              </span>
            </h1>
            <p className="text-xl text-gray-300">
              {CONFIG.personal.bio}
            </p>
            <div className="flex gap-4">
              <a
                href={CONFIG.personal.robloxProfile}
                target="_blank"
                rel="noopener noreferrer"
                className="px-8 py-3 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg font-semibold hover:scale-105 transition-transform flex items-center gap-2"
              >
                View Roblox Profile <ExternalLink size={18} />
              </a>
              <button
                onClick={() => document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })}
                className="px-8 py-3 border-2 border-blue-500 rounded-lg font-semibold hover:bg-blue-500/20 transition-colors"
              >
                Contact Me
              </button>
            </div>
          </div>
          <div className="relative">
            <div className="absolute inset-0 bg-gradient-to-r from-blue-500 to-purple-600 rounded-full blur-3xl opacity-30"></div>
            <img
              src={CONFIG.personal.avatar}
              alt="Avatar"
              className="relative w-full max-w-md mx-auto rounded-2xl shadow-2xl"
            />
          </div>
        </div>
      </section>

      {/* Stats Section */}
      <section className="py-20 px-6 bg-slate-800/50">
        <div className="max-w-6xl mx-auto grid grid-cols-2 md:grid-cols-4 gap-8">
          {CONFIG.stats.map((stat, i) => {
            const IconComponent = iconMap[stat.icon] || Users;
            return (
              <div key={i} className="text-center space-y-3 p-6 bg-slate-900/50 rounded-xl hover:bg-slate-900/70 transition-colors">
                <IconComponent className="w-12 h-12 mx-auto text-blue-400" />
                <div className="text-3xl font-bold text-blue-400">{stat.value}</div>
                <div className="text-gray-400">{stat.label}</div>
              </div>
            );
          })}
        </div>
      </section>

      {/* Featured Games */}
      <section id="games" className="py-20 px-6">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-4xl font-bold mb-12 text-center">Featured Games</h2>
          <div className="grid md:grid-cols-2 gap-8">
            {featuredGames.map((game, i) => (
              <div key={i} className="group relative bg-slate-800/50 rounded-xl overflow-hidden hover:scale-105 transition-transform">
                <img src={game.image} alt={game.title} className="w-full h-48 object-cover" />
                <div className="p-6 space-y-3">
                  <h3 className="text-2xl font-bold">{game.title}</h3>
                  <p className="text-gray-400">{game.description}</p>
                  <div className="flex items-center justify-between text-sm">
                    <span className="text-blue-400">👥 {game.visits} visits</span>
                    <span className="text-green-400">⭐ {game.rating} rating</span>
                  </div>
                  <a
                    href={game.link}
                    target="_blank"
                    rel="noopener noreferrer"
                    className="inline-flex items-center gap-2 px-6 py-2 bg-blue-500 rounded-lg hover:bg-blue-600 transition-colors"
                  >
                    Play Now <ExternalLink size={16} />
                  </a>
                </div>
              </div>
            ))}
          </div>
          
          {/* All Games */}
          <div className="mt-12 space-y-4">
            <h3 className="text-2xl font-bold">All Projects</h3>
            {CONFIG.games.map((game, i) => (
              <div key={i} className="p-4 bg-slate-800/30 rounded-lg flex items-center justify-between hover:bg-slate-800/50 transition-colors">
                <div>
                  <div className="font-semibold">{game.title}</div>
                  <div className="text-sm text-gray-400">{game.visits} visits • {game.rating} rating</div>
                </div>
                <a
                  href={game.link}
                  target="_blank"
                  rel="noopener noreferrer"
                  className="px-4 py-2 bg-blue-500/20 hover:bg-blue-500 rounded-lg transition-colors"
                >
                  View
                </a>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Skills Section */}
      <section id="skills" className="py-20 px-6 bg-slate-800/50">
        <div className="max-w-4xl mx-auto">
          <h2 className="text-4xl font-bold mb-12 text-center">Skills & Expertise</h2>
          <div className="space-y-6">
            {CONFIG.skills.map((skill, i) => (
              <div key={i} className="space-y-2">
                <div className="flex justify-between text-sm">
                  <span className="font-semibold">{skill.name}</span>
                  <span className="text-blue-400">{skill.level}%</span>
                </div>
                <div className="h-3 bg-slate-700 rounded-full overflow-hidden">
                  <div
                    className="h-full bg-gradient-to-r from-blue-500 to-purple-600 rounded-full transition-all duration-1000"
                    style={{ width: `${skill.level}%` }}
                  ></div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Contact Section */}
      <section id="contact" className="py-20 px-6">
        <div className="max-w-4xl mx-auto text-center space-y-8">
          <h2 className="text-4xl font-bold">Let's Work Together</h2>
          <p className="text-xl text-gray-400">
            Interested in collaborating or have a project in mind? Get in touch!
          </p>
          <div className="grid md:grid-cols-2 gap-6 max-w-2xl mx-auto">
            <a
              href={`mailto:${CONFIG.contact.email}`}
              className="p-6 bg-slate-800/50 rounded-xl hover:bg-slate-800 transition-colors flex items-center gap-4"
            >
              <Mail className="w-8 h-8 text-blue-400" />
              <div className="text-left">
                <div className="font-semibold">Email</div>
                <div className="text-sm text-gray-400">{CONFIG.contact.email}</div>
              </div>
            </a>
            <div className="p-6 bg-slate-800/50 rounded-xl hover:bg-slate-800 transition-colors flex items-center gap-4">
              <MessageSquare className="w-8 h-8 text-purple-400" />
              <div className="text-left">
                <div className="font-semibold">Discord</div>
                <div className="text-sm text-gray-400">{CONFIG.contact.discord}</div>
              </div>
            </div>
          </div>
          <div className="flex justify-center gap-6 pt-8">
            {CONFIG.contact.github && (
              <a
                href={CONFIG.contact.github}
                target="_blank"
                rel="noopener noreferrer"
                className="w-12 h-12 flex items-center justify-center bg-slate-800 rounded-full hover:bg-blue-500 transition-colors"
              >
                <Github size={24} />
              </a>
            )}
            {CONFIG.contact.twitter && (
              <a
                href={CONFIG.contact.twitter}
                target="_blank"
                rel="noopener noreferrer"
                className="w-12 h-12 flex items-center justify-center bg-slate-800 rounded-full hover:bg-blue-500 transition-colors"
              >
                <svg className="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
                </svg>
              </a>
            )}
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-8 px-6 bg-slate-900 text-center text-gray-400">
        <p>© 2025 {CONFIG.personal.name}. All rights reserved.</p>
        <p className="text-sm mt-2">Made with ❤️ for Roblox Developers</p>
      </footer>
    </div>
  );
}
