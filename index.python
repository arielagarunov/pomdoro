import React, { useState, useEffect, useRef } from 'react';

// Define our "Ghost" Personalities
const AGENTS = [
  { id: 'skeptic', name: 'Silas the Skeptic', color: '#ff4d4d', prompt: 'You are doubtful and clinical.' },
  { id: 'muse', name: 'Mina the Muse', color: '#4da6ff', prompt: 'You are poetic and inspiring.' },
  { id: 'shadow', name: 'The Shadow', color: '#808080', prompt: 'You speak in cryptic, short sentences.' }
];

export default function PhantomForum() {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState('');
  const [isTyping, setIsTyping] = useState(null);
  const scrollRef = useRef(null);

  // Auto-scroll to bottom
  useEffect(() => {
    scrollRef.current?.scrollIntoView({ behavior: 'smooth' });
  }, [messages, isTyping]);

  const handleSend = async (e) => {
    e.preventDefault();
    if (!input.trim()) return;

    const userMsg = { role: 'user', content: input, sender: 'You' };
    setMessages(prev => [...prev, userMsg]);
    setInput('');

    // Trigger AI Agents one by one
    for (const agent of AGENTS) {
      setIsTyping(agent.name);
      
      // Simulate API Delay
      await new Promise(resolve => setTimeout(resolve, 1500));
      
      const aiMsg = {
        role: 'assistant',
        content: `[Simulated ${agent.name} response to: "${input}"]`,
        sender: agent.name,
        color: agent.color
      };
      
      setMessages(prev => [...prev, aiMsg]);
      setIsTyping(null);
    }
  };

  return (
    <div style={{ maxWidth: '600px', margin: '0 auto', padding: '20px', fontFamily: 'monospace', backgroundColor: '#1a1a1a', color: '#e0e0e0', minHeight: '100vh' }}>
      <header style={{ borderBottom: '1px solid #333', paddingBottom: '10px' }}>
        <h1>THE PHANTOM FORUM</h1>
        <p>You are not alone here.</p>
      </header>

      <div style={{ height: '70vh', overflowY: 'auto', padding: '20px 0' }}>
        {messages.map((msg, i) => (
          <div key={i} style={{ marginBottom: '15px', borderLeft: `3px solid ${msg.color || '#fff'}`, paddingLeft: '10px' }}>
            <strong style={{ color: msg.color || '#fff' }}>{msg.sender}:</strong>
            <p style={{ margin: '5px 0' }}>{msg.content}</p>
          </div>
        ))}
        {isTyping && <div style={{ fontStyle: 'italic', color: '#888' }}>{isTyping} is whispering...</div>}
        <div ref={scrollRef} />
      </div>

      <form onSubmit={handleSend} style={{ display: 'flex', gap: '10px' }}>
        <input 
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="Speak to the void..."
          style={{ flex: 1, padding: '10px', background: '#333', border: 'none', color: '#fff' }}
        />
        <button type="submit" style={{ padding: '10px 20px', cursor: 'pointer', background: '#444', color: '#fff', border: '1px solid #666' }}>Send</button>
      </form>
    </div>
  );
}
