/ FILE: client/src/App.tsx
import { Switch, Route } from "wouter";
import { queryClient } from "./lib/queryClient";
import { QueryClientProvider } from "@tanstack/react-query";
import { Toaster } from "@/components/ui/toaster";
import { TooltipProvider } from "@/components/ui/tooltip";
import Home from "@/pages/Home";
import NotFound from "@/pages/not-found";
function Router() {
  return (
    <Switch>
      {/* Add pages below */}
      <Route path="/" component={Home} />
      {/* Fallback to 404 */}
      <Route component={NotFound} />
    </Switch>
  );
}
function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <TooltipProvider>
        <Toaster />
        <Router />
      </TooltipProvider>
    </QueryClientProvider>
  );
}
export default App;
// FILE: client/src/pages/Home.tsx
import { Sidebar } from "@/components/Sidebar";
import { SecretForm } from "@/components/SecretForm";
import { SecretsList } from "@/components/SecretsList";
import { useQuery } from "@tanstack/react-query";
import { Secret } from "@shared/schema";
import { useState, useEffect } from "react";
const Home = () => {
  // Animation state
  const [showPage, setShowPage] = useState(false);
  
  // Fetch all secrets
  const { data: secrets, isLoading, isError } = useQuery<Secret[]>({
    queryKey: ['/api/secrets'],
  });
  
  // Animation on mount
  useEffect(() => {
    const timer = setTimeout(() => {
      setShowPage(true);
    }, 100);
    return () => clearTimeout(timer);
  }, []);
  return (
    <div className={`bg-[#050505] text-white min-h-screen flex flex-col transition-all duration-700 relative overflow-hidden ${showPage ? 'opacity-100' : 'opacity-0'}`}>
      {/* Background overlay with film grain texture */}
      <div className="absolute inset-0 bg-gradient-to-b from-[#0a0a0a] to-[#000000] opacity-95"></div>
      <div className="absolute inset-0 bg-[url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIzMDAiIGhlaWdodD0iMzAwIj48ZmlsdGVyIGlkPSJhIiB4PSIwIiB5PSIwIj48ZmVUdXJidWxlbmNlIGJhc2VGcmVxdWVuY3k9Ii43NSIgc3RpdGNoVGlsZXM9InN0aXRjaCIgdHlwZT0iZnJhY3RhbE5vaXNlIi8+PGZlQ29sb3JNYXRyaXggdHlwZT0ic2F0dXJhdGUiIHZhbHVlcz0iMCIvPjwvZmlsdGVyPjxwYXRoIGQ9Ik0wIDBoMzAwdjMwMEgweiIgZmlsdGVyPSJ1cmwoI2EpIiBvcGFjaXR5PSIuMDUiLz48L3N2Zz4=')]"></div>
      
      {/* Radial gradient overlays */}
      <div className="absolute inset-0 bg-[radial-gradient(ellipse_at_top_right,rgba(255,94,0,0.05),transparent_80%)]"></div>
      <div className="absolute inset-0 bg-[radial-gradient(ellipse_at_bottom_left,rgba(255,255,255,0.03),transparent_70%)]"></div>
      
      {/* Dynamic light beams */}
      <div className="absolute top-20 right-10 w-[500px] h-[500px] bg-[#ff5e00]/3 blur-[180px] rounded-full animate-pulse"></div>
      <div className="absolute -bottom-40 left-1/4 w-[500px] h-[500px] bg-white/3 blur-[180px] rounded-full animate-pulse" style={{ animationDelay: '2s' }}></div>
      
      {/* Grid pattern */}
      <div className="absolute inset-0 bg-[linear-gradient(rgba(255,255,255,0.02)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.02)_1px,transparent_1px)] bg-[size:100px_100px] [mask-image:radial-gradient(ellipse_80%_80%_at_50%_50%,#000_40%,transparent_100%)]"></div>
      {/* Elegant top navigation */}
      <nav className="relative z-20 flex items-center justify-between px-8 md:px-16 py-5 border-b border-white/5 backdrop-blur-sm">
        <div className="flex items-center">
          <h2 className="text-lg md:text-xl font-medium tracking-widest">
            <span className="font-extralight text-white/80">Secrets of</span> <span className="font-bold text-white ml-1">Inner Code</span>
          </h2>
        </div>
        
        <div className="hidden md:flex items-center space-x-12">
          <a href="#" className="group text-white/70 hover:text-white text-sm uppercase tracking-wider relative py-2">
            <span>Home</span>
            <span className="absolute bottom-0 left-0 w-0 h-[1px] bg-[#ff5e00] group-hover:w-full transition-all duration-300"></span>
          </a>
          <a href="#" className="group text-white/70 hover:text-white text-sm uppercase tracking-wider relative py-2">
            <span>Explore</span>
            <span className="absolute bottom-0 left-0 w-0 h-[1px] bg-[#ff5e00] group-hover:w-full transition-all duration-300"></span>
          </a>
          <a href="#" className="group text-white/70 hover:text-white text-sm uppercase tracking-wider relative py-2">
            <span>Popular</span>
            <span className="absolute bottom-0 left-0 w-0 h-[1px] bg-[#ff5e00] group-hover:w-full transition-all duration-300"></span>
          </a>
          <a href="#" className="group text-white/70 hover:text-white text-sm uppercase tracking-wider relative py-2">
            <span>About</span>
            <span className="absolute bottom-0 left-0 w-0 h-[1px] bg-[#ff5e00] group-hover:w-full transition-all duration-300"></span>
          </a>
        </div>
        
        <div className="flex items-center">
          <button className="md:hidden text-white/80 hover:text-white">
            <i className="ri-menu-line text-xl"></i>
          </button>
          <button className="hidden md:flex items-center space-x-2 text-white/70 hover:text-white border border-white/10 hover:border-white/20 px-4 py-2 rounded-full text-sm transition-all duration-300">
            <i className="ri-user-line"></i>
            <span>Sign In</span>
          </button>
        </div>
      </nav>
      {/* Hero section with parallax effect */}
      <header className="relative z-10 py-16 md:py-24 px-8 md:px-16 text-center">
        <h1 className="font-['Playfair_Display'] font-extrabold text-5xl md:text-7xl lg:text-8xl text-white mb-5 tracking-wide relative inline-block">
          <span className="opacity-0 animate-fadeIn" style={{ animationDelay: '0.3s', animationFillMode: 'forwards' }}>Inner</span>
          <span className="mx-2 opacity-0 animate-fadeIn" style={{ animationDelay: '0.6s', animationFillMode: 'forwards' }}>Code</span>
        </h1>
        
        <div className="flex justify-center mb-5">
          <div className="w-32 md:w-40 h-1 bg-[#ff5e00] rounded-full opacity-0 animate-fadeIn" style={{ animationDelay: '0.9s', animationFillMode: 'forwards' }}></div>
        </div>
        
        <p className="font-['Playfair_Display'] text-white/80 text-lg md:text-xl max-w-2xl mx-auto opacity-0 animate-fadeIn" style={{ animationDelay: '1.2s', animationFillMode: 'forwards' }}>
          Secrets that changed lives — shared softly, safely.
        </p>
        
        <div className="mt-10 inline-flex items-center justify-center gap-4 opacity-0 animate-fadeIn" style={{ animationDelay: '1.5s', animationFillMode: 'forwards' }}>
          <button className="group flex items-center space-x-2 bg-transparent border border-white/20 hover:border-[#ff5e00] px-7 py-3 rounded-full text-white/90 hover:text-white transition-all duration-300">
            <span>Discover Stories</span>
            <span className="group-hover:translate-x-1 transition-transform duration-300 text-[#ff5e00]">→</span>
          </button>
          
          <button className="flex items-center space-x-2 bg-black/30 backdrop-blur-md border border-white/10 px-4 py-3 rounded-full text-white/80 hover:text-white hover:bg-black/40 transition-all duration-300">
            <i className="ri-play-circle-line text-[#ff5e00]"></i>
            <span>Watch Story</span>
          </button>
        </div>
      </header>
      {/* Main Layout */}
      <div className="flex flex-col md:flex-row flex-1 relative z-10">
        <Sidebar />
        <main className="flex-1 p-6 md:p-12 lg:p-16 bg-gradient-to-b from-black/80 to-black/40 backdrop-blur-sm border-l border-white/5">
          {/* Scroll indicator */}
          <div className="hidden lg:flex items-center justify-center fixed top-1/2 right-8 flex-col">
            <div className="w-0.5 h-20 bg-white/10"></div>
            <div className="text-xs uppercase tracking-widest text-white/50 transform rotate-90 origin-center mt-4">Scroll to explore</div>
          </div>
          
          <SecretForm />
          <SecretsList secrets={secrets || []} isLoading={isLoading} isError={isError} />
        </main>
      </div>
      
      {/* Footer with social icons */}
      <footer className="relative z-10 py-6 px-8 md:px-16 border-t border-white/5 backdrop-blur-sm">
        <div className="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
          <div className="text-sm text-white/50 flex items-center space-x-4">
            <span>© 2025 Inner Code</span>
            <span className="hidden md:inline text-white/20">|</span>
            <a href="#" className="hover:text-white/80 transition-colors duration-200">Privacy</a>
            <a href="#" className="hover:text-white/80 transition-colors duration-200">Terms</a>
          </div>
          
          <div className="flex items-center space-x-6">
            <a href="#" className="text-white/40 hover:text-[#ff5e00] transition-colors duration-200">
              <i className="ri-instagram-line text-lg"></i>
            </a>
            <a href="#" className="text-white/40 hover:text-[#ff5e00] transition-colors duration-200">
              <i className="ri-facebook-circle-line text-lg"></i>
            </a>
            <a href="#" className="text-white/40 hover:text-[#ff5e00] transition-colors duration-200">
              <i className="ri-twitter-x-line text-lg"></i>
            </a>
            <a href="#" className="text-white/40 hover:text-[#ff5e00] transition-colors duration-200">
              <i className="ri-pinterest-line text-lg"></i>
            </a>
          </div>
        </div>
      </footer>
      
      {/* Additional decorative elements */}
      <div className="hidden lg:block absolute top-1/4 left-0 w-[150px] h-[1px] bg-gradient-to-r from-[#ff5e00]/30 to-transparent opacity-50"></div>
      <div className="hidden lg:block absolute bottom-1/4 right-0 w-[150px] h-[1px] bg-gradient-to-l from-[#ff5e00]/30 to-transparent opacity-50"></div>
    </div>
  );
};
export default Home;
// FILE: client/src/components/Sidebar.tsx
import { useLocation } from "wouter";
import { useState, useEffect } from "react";
export const Sidebar = () => {
  const [location] = useLocation();
  const [activeItem, setActiveItem] = useState("#home");
  const [isMounted, setIsMounted] = useState(false);
  useEffect(() => {
    setIsMounted(true);
  }, []);
  const navItems = [
    { href: "#home", icon: "ri-home-line", text: "Home", delay: 100 },
    { href: "#categories", icon: "ri-bookmark-line", text: "Categories", delay: 200 },
    { href: "#post-secret", icon: "ri-quill-pen-line", text: "Post a Secret", delay: 300 },
    { href: "#profile", icon: "ri-user-line", text: "Profile", delay: 400 },
    { href: "#search", icon: "ri-search-line", text: "Search", delay: 500 },
    { href: "#settings", icon: "ri-settings-3-line", text: "Settings", delay: 600 },
  ];
  const handleNavClick = (href: string) => {
    setActiveItem(href);
  };
  return (
    <aside className="bg-black/60 backdrop-blur-md w-full md:w-64 border-r border-white/5 md:min-h-screen transition-all duration-500 relative overflow-hidden">
      {/* Film grain texture overlay */}
      <div className="absolute inset-0 opacity-20 pointer-events-none bg-[url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIzMDAiIGhlaWdodD0iMzAwIj48ZmlsdGVyIGlkPSJhIiB4PSIwIiB5PSIwIj48ZmVUdXJidWxlbmNlIGJhc2VGcmVxdWVuY3k9Ii43NSIgc3RpdGNoVGlsZXM9InN0aXRjaCIgdHlwZT0iZnJhY3RhbE5vaXNlIi8+PGZlQ29sb3JNYXRyaXggdHlwZT0ic2F0dXJhdGUiIHZhbHVlcz0iMCIvPjwvZmlsdGVyPjxwYXRoIGQ9Ik0wIDBoMzAwdjMwMEgweiIgZmlsdGVyPSJ1cmwoI2EpIiBvcGFjaXR5PSIuMDUiLz48L3N2Zz4=')]"></div>
      
      {/* Background gradient effects */}
      <div className="absolute top-0 right-0 w-full h-40 bg-gradient-to-b from-[#ff5e00]/10 to-transparent opacity-50"></div>
      <div className="absolute bottom-0 left-0 w-full h-40 bg-gradient-to-t from-[#ff5e00]/5 to-transparent opacity-30"></div>
      
      {/* Top accent line */}
      <div className="h-1 w-full bg-gradient-to-r from-transparent via-[#ff5e00] to-transparent"></div>
      
      {/* Logo section */}
      <div className="relative p-6 flex items-center justify-center mb-4 border-b border-white/5">
        <div className="flex items-center justify-center">
          <div className={`w-10 h-10 rounded-full bg-black/80 border border-[#ff5e00]/40 flex items-center justify-center shadow-[0_0_15px_rgba(255,94,0,0.2)] transition-opacity duration-1000 ${isMounted ? 'opacity-100' : 'opacity-0'}`}>
            <span className="text-white font-semibold text-xl">IC</span>
          </div>
          <div className={`ml-3 transition-all duration-700 delay-300 ${isMounted ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-4'}`}>
            <h3 className="text-white font-medium tracking-wide text-sm">Inner Code</h3>
            <div className="w-16 h-0.5 bg-gradient-to-r from-[#ff5e00] to-transparent mt-1"></div>
          </div>
        </div>
      </div>
      
      {/* Navigation items with staggered animation */}
      <div className="p-4">
        {navItems.map((item, index) => (
          <a
            key={item.text}
            href={item.href}
            onClick={() => handleNavClick(item.href)}
            className={`
              group flex items-center no-underline text-sm py-3 px-4 my-2.5
              rounded-lg transition-all duration-300 relative overflow-hidden
              ${isMounted ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-4'}
              ${activeItem === item.href 
                ? "bg-black/40 text-white border border-[#ff5e00]/20" 
                : "text-white/70 hover:text-white hover:bg-black/20"}
            `}
            style={{ 
              transitionDelay: `${item.delay}ms`,
              backdropFilter: 'blur(8px)'
            }}
          >
            <div className={`
              flex items-center justify-center w-8 h-8 rounded-full mr-3 transition-all duration-300
              ${activeItem === item.href
                ? "bg-black text-[#ff5e00] border border-[#ff5e00]/30" 
                : "bg-black/60 text-white/80 border border-white/10 group-hover:border-white/30"}
            `}>
              <i className={`${item.icon} ${activeItem === item.href ? 'text-[#ff5e00]' : 'text-white/80 group-hover:text-white'}`}></i>
            </div>
            
            <span className="font-medium tracking-wide">{item.text}</span>
            
            {/* Hover and active indicators */}
            {activeItem === item.href && (
              <div className="absolute -right-1 top-1/2 -translate-y-1/2 w-1.5 h-1.5 rounded-full bg-[#ff5e00]"></div>
            )}
            
            {/* Bottom indicator */}
            <div className={`
              absolute bottom-0 left-0 w-0 h-0.5 bg-[#ff5e00]/50
              ${activeItem === item.href ? 'w-full' : 'group-hover:w-full'}
              transition-all duration-500 ease-out
            `}></div>
            
            {/* Background hover effect */}
            <div className="absolute inset-0 opacity-0 group-hover:opacity-100 pointer-events-none transition-opacity duration-500 bg-gradient-to-r from-transparent via-[#ff5e00]/5 to-transparent"></div>
          </a>
        ))}
      </div>
      
      {/* User profile section */}
      <div className="absolute bottom-0 left-0 right-0 p-4 border-t border-white/5 backdrop-blur-sm bg-black/20">
        <div className={`flex items-center space-x-3 transition-all duration-700 delay-700 ${isMounted ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}`}>
          <div className="w-9 h-9 rounded-full bg-black/60 border border-white/20 flex items-center justify-center text-white">
            <i className="ri-user-line"></i>
          </div>
          <div>
            <p className="text-white text-xs font-medium">Guest User</p>
            <p className="text-white/50 text-xs">Sign in for more</p>
          </div>
          <button className="ml-auto w-8 h-8 rounded-full bg-black/40 border border-white/10 flex items-center justify-center text-white/70 hover:text-white hover:border-white/30 transition-all duration-300">
            <i className="ri-logout-box-line text-sm"></i>
          </button>
        </div>
      </div>
      
      {/* Decorative elements */}
      <div className="absolute top-1/3 left-0 w-full">
        <div className="w-2 h-10 bg-gradient-to-b from-[#ff5e00]/30 to-transparent opacity-20"></div>
      </div>
      
      <div className="absolute bottom-1/4 right-0">
        <div className="w-1 h-20 bg-gradient-to-t from-[#ff5e00]/20 to-transparent opacity-20"></div>
      </div>
    </aside>
  );
};
// FILE: client/src/components/SecretForm.tsx
import { useState } from "react";
import { useMutation } from "@tanstack/react-query";
import { apiRequest, queryClient } from "@/lib/queryClient";
import { categories } from "@shared/schema";
import { useToast } from "@/hooks/use-toast";
export const SecretForm = () => {
  const { toast } = useToast();
  const [formData, setFormData] = useState({
    category: "Mental Health",
    text: "",
    anonymous: false,
  });
  const secretMutation = useMutation({
    mutationFn: async (data: typeof formData) => {
      const response = await apiRequest("POST", "/api/secrets", data);
      return response.json();
    },
    onSuccess: () => {
      // Reset form and invalidate cache to refresh the list
      setFormData({
        category: "Mental Health",
        text: "",
        anonymous: false,
      });
      queryClient.invalidateQueries({ queryKey: ['/api/secrets'] });
      
      toast({
        title: "Secret shared",
        description: "Your wisdom has been added to the community.",
      });
    },
    onError: (error) => {
      toast({
        title: "Failed to share secret",
        description: error.message || "Please try again.",
        variant: "destructive",
      });
    },
  });
  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    
    if (!formData.text.trim()) {
      toast({
        title: "Cannot share empty secret",
        description: "Please write something to share with the community.",
        variant: "destructive",
      });
      return;
    }
    
    secretMutation.mutate(formData);
  };
  return (
    <section className="mb-16 relative">
      <div className="relative mb-10">
        <h2 className="font-['Playfair_Display'] font-bold text-3xl text-white relative inline-block">
          Share Your Secret
        </h2>
        <div className="absolute -bottom-3 left-0 w-24 h-1 bg-[#ff5e00] rounded-full"></div>
      </div>
      
      <form onSubmit={handleSubmit} className="space-y-8 bg-black/40 backdrop-blur-sm p-8 rounded-lg border border-white/5 shadow-[0_15px_40px_rgba(0,0,0,0.3)] relative">
        {/* Corner decoration like Idliez */}
        <div className="absolute top-0 right-0 w-16 h-16">
          <div className="absolute top-0 right-0 w-8 h-8 border-t border-r border-white/10"></div>
        </div>
        
        <div className="relative">
          <label className="block text-white/70 text-sm uppercase tracking-wider mb-2 font-medium">Select Category</label>
          <div className="relative">
            <select
              id="category"
              value={formData.category}
              onChange={(e) => setFormData({ ...formData, category: e.target.value })}
              className="w-full py-4 px-5 rounded-lg border border-white/10 bg-black/70 text-white appearance-none cursor-pointer focus:border-[#ff5e00] focus:outline-none transition-all duration-200"
            >
              {categories.map((category) => (
                <option key={category} value={category} className="bg-[#050505] text-white">
                  {category}
                </option>
              ))}
            </select>
            <div className="absolute right-4 top-1/2 -translate-y-1/2 pointer-events-none">
              <i className="ri-arrow-down-s-line text-[#ff5e00] text-lg"></i>
            </div>
          </div>
        </div>
        
        <div className="relative group">
          <label className="block text-white/70 text-sm uppercase tracking-wider mb-2 font-medium">Your Secret</label>
          <textarea
            id="secretInput"
            value={formData.text}
            onChange={(e) => setFormData({ ...formData, text: e.target.value })}
            rows={4}
            placeholder="Write a secret that truly helped you..."
            className="w-full p-5 rounded-lg border border-white/10 bg-black/70 text-white min-h-[160px] resize-y focus:border-[#ff5e00] focus:outline-none transition-all duration-200"
          />
        </div>
        
        <div className="flex items-center justify-between">
          <label className="flex items-center space-x-3 py-2 cursor-pointer group">
            <div className="relative">
              <input
                type="checkbox"
                id="anonymous"
                checked={formData.anonymous}
                onChange={(e) => setFormData({ ...formData, anonymous: e.target.checked })}
                className="sr-only peer"
              />
              <div className="w-5 h-5 border border-white/20 rounded-sm bg-black/50 peer-checked:bg-[#ff5e00] peer-checked:border-[#ff5e00] transition-all duration-200"></div>
              <i className="ri-check-line absolute text-black text-sm left-[3px] top-[2px] opacity-0 peer-checked:opacity-100 transition-opacity"></i>
            </div>
            <span className="text-white/70 group-hover:text-white transition-colors">Post anonymously</span>
          </label>
          
          <button
            type="submit"
            disabled={secretMutation.isPending}
            className="group relative overflow-hidden px-8 py-3 rounded-full bg-transparent border border-white/20 text-white font-medium hover:border-[#ff5e00] transition-all duration-300 focus:outline-none disabled:opacity-50 disabled:cursor-not-allowed"
          >
            <span className="relative z-10 flex items-center space-x-2">
              <span>{secretMutation.isPending ? "Sharing..." : "Share Secret"}</span>
              <span className="group-hover:translate-x-1 transition-transform duration-300 text-[#ff5e00]">→</span>
            </span>
          </button>
        </div>
      </form>
      
      {/* Scroll element like Idliez */}
      <div className="hidden md:flex justify-center mt-12">
        <div className="flex flex-col items-center">
          <div className="w-0.5 h-8 bg-white/10"></div>
          <div className="w-1.5 h-1.5 rounded-full bg-[#ff5e00] mt-1"></div>
        </div>
      </div>
    </section>
  );
};
// FILE: client/src/components/Secret.tsx
import { useMutation } from "@tanstack/react-query";
import { apiRequest, queryClient } from "@/lib/queryClient";
import { Secret } from "@shared/schema";
import { useToast } from "@/hooks/use-toast";
import { useState } from "react";
interface SecretItemProps {
  secret: Secret;
}
export const SecretItem = ({ secret }: SecretItemProps) => {
  const { toast } = useToast();
  const [isHovered, setIsHovered] = useState(false);
  
  // Format the timestamp to a readable format
  const formatTimestamp = (timestamp: Date) => {
    const date = new Date(timestamp);
    return date.toLocaleString(undefined, {
      hour: 'numeric',
      minute: 'numeric',
      hour12: true,
      day: 'numeric',
      month: 'short'
    });
  };
  const likeMutation = useMutation({
    mutationFn: async () => {
      const response = await apiRequest("POST", `/api/secrets/${secret.id}/like`, {});
      return response.json();
    },
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['/api/secrets'] });
      toast({
        title: "Wisdom appreciated",
        description: "You've acknowledged this secret's impact.",
      });
    },
    onError: (error) => {
      toast({
        title: "Failed to appreciate",
        description: error.message || "Please try again.",
        variant: "destructive",
      });
    },
  });
  const handleLike = () => {
    likeMutation.mutate();
  };
  // Get a deterministic random number based on the secret id for subtle visual variations
  const getRandomOffset = (min: number, max: number) => {
    const randomVal = (secret.id * 9301 + 49297) % 233280;
    return min + (randomVal / 233280) * (max - min);
  };
  return (
    <article 
      className="group bg-black/40 backdrop-blur-sm rounded-lg overflow-hidden shadow-[0_15px_40px_rgba(0,0,0,0.3)] relative hover:shadow-[0_20px_50px_rgba(0,0,0,0.4)] transition-all duration-500"
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
      style={{ 
        transform: isHovered ? 'translateY(-5px)' : 'translateY(0)',
        transitionTimingFunction: 'cubic-bezier(0.34, 1.56, 0.64, 1)'
      }}
    >
      {/* Background gradient effect */}
      <div 
        className="absolute inset-0 opacity-0 group-hover:opacity-100 transition-opacity duration-1000 pointer-events-none"
        style={{
          background: `radial-gradient(circle at ${getRandomOffset(30, 70)}% ${getRandomOffset(30, 70)}%, rgba(255, 94, 0, 0.05) 0%, transparent 70%)`
        }}
      ></div>
      
      {/* Corner decoration like Idliez */}
      <div className="absolute top-0 right-0 w-16 h-16">
        <div className="absolute top-0 right-0 w-8 h-8 border-t border-r border-white/10 group-hover:border-[#ff5e00]/20 transition-colors duration-500"></div>
      </div>
      <div className="absolute bottom-0 left-0 w-16 h-16">
        <div className="absolute bottom-0 left-0 w-8 h-8 border-b border-l border-white/10 group-hover:border-[#ff5e00]/20 transition-colors duration-500"></div>
      </div>
      <div className="p-6 md:p-8 border-b border-white/5">
        {/* Category with glow effect */}
        <div className="relative inline-block">
          <div className="inline-block bg-black/50 text-[#ff5e00] uppercase tracking-wider text-xs font-medium py-1 px-3 rounded-full border border-white/10 group-hover:border-[#ff5e00]/30 mb-6 transition-all duration-500">
            {secret.category}
          </div>
          <div className="absolute inset-0 bg-[#ff5e00]/5 blur-md rounded-full opacity-0 group-hover:opacity-100 transition-opacity duration-500" style={{ filter: 'blur(8px)' }}></div>
        </div>
        
        {/* Quote decoration */}
        <div className="absolute top-10 right-10 text-[#ff5e00]/10 text-5xl font-serif opacity-0 group-hover:opacity-30 transition-opacity duration-500">"</div>
        
        {/* Secret text with line animation */}
        <div className="relative">
          <p className="text-white/90 leading-relaxed">
            {secret.text}
          </p>
          <div className="absolute left-0 top-0 w-1 h-0 group-hover:h-full bg-gradient-to-b from-transparent via-[#ff5e00]/20 to-transparent transition-all duration-700 ease-out" style={{ transitionDelay: '200ms' }}></div>
        </div>
      </div>
      
      {/* Information and actions */}
      <div className="px-6 py-4 md:px-8 md:py-4 flex items-center justify-between">
        <div className="text-white/50 text-sm font-light">
          {secret.anonymous ? 'Shared Anonymously' : 'From a community member'} • {formatTimestamp(secret.timestamp)}
        </div>
        
        <button 
          className="group/btn flex items-center space-x-2 focus:outline-none"
          onClick={handleLike}
          disabled={likeMutation.isPending}
        >
          <div className="w-8 h-8 rounded-full border border-white/10 flex items-center justify-center hover:border-[#ff5e00] group-hover:bg-[#ff5e00]/5 transition-all duration-300">
            <i className={`${likeMutation.isPending ? 'ri-loader-2-line animate-spin' : 'ri-heart-line group-hover/btn:text-[#ff5e00]'} text-white/70 transition-all duration-300`}></i>
          </div>
          <span className="text-white/70 group-hover/btn:text-white transition-colors">{secret.likes}</span>
        </button>
      </div>
      
      {/* Hover indicator like Idliez */}
      <div className="absolute bottom-0 left-0 w-0 h-1 bg-[#ff5e00] group-hover:w-full transition-all duration-500 ease-out"></div>
    </article>
  );
};
// FILE: client/src/components/SecretsList.tsx
import { Secret } from "@shared/schema";
import { SecretItem } from "./Secret";
import { Skeleton } from "@/components/ui/skeleton";
interface SecretsListProps {
  secrets: Secret[];
  isLoading: boolean;
  isError: boolean;
}
export const SecretsList = ({ secrets, isLoading, isError }: SecretsListProps) => {
  // Loading state
  if (isLoading) {
    return (
      <section className="relative">
        <div className="relative mb-10">
          <h2 className="font-['Playfair_Display'] font-bold text-3xl text-white relative inline-block">
            Inner Wisdom Shared
          </h2>
          <div className="absolute -bottom-3 left-0 w-24 h-1 bg-[#ff5e00] rounded-full"></div>
        </div>
        
        <div className="space-y-8">
          {[1, 2, 3].map((i) => (
            <div key={i} className="bg-black/40 backdrop-blur-sm rounded-lg overflow-hidden shadow-[0_15px_40px_rgba(0,0,0,0.3)] relative">
              <div className="p-6 md:p-8 border-b border-white/5">
                <Skeleton className="h-6 w-24 bg-white/10 mb-6" />
                <Skeleton className="h-4 w-full bg-white/5 mb-3" />
                <Skeleton className="h-4 w-full bg-white/5 mb-3" />
                <Skeleton className="h-4 w-2/3 bg-white/5 mb-4" />
              </div>
              
              <div className="px-6 py-4 md:px-8 md:py-4 flex items-center justify-between">
                <Skeleton className="h-4 w-40 bg-white/5" />
                <Skeleton className="h-8 w-16 rounded-full bg-white/10" />
              </div>
              
              {/* Corner decoration like Idliez */}
              <div className="absolute top-0 right-0 w-16 h-16">
                <div className="absolute top-0 right-0 w-8 h-8 border-t border-r border-white/10"></div>
              </div>
            </div>
          ))}
        </div>
      </section>
    );
  }
  // Error state
  if (isError) {
    return (
      <section className="relative">
        <div className="relative mb-10">
          <h2 className="font-['Playfair_Display'] font-bold text-3xl text-white relative inline-block">
            Inner Wisdom Shared
          </h2>
          <div className="absolute -bottom-3 left-0 w-24 h-1 bg-[#ff5e00] rounded-full"></div>
        </div>
        
        <div className="bg-black/40 backdrop-blur-sm rounded-lg p-12 text-center shadow-[0_15px_40px_rgba(0,0,0,0.3)] border border-white/5">
          <div className="inline-flex items-center justify-center w-16 h-16 rounded-full bg-black/50 border border-red-500/30 mb-6">
            <i className="ri-error-warning-line text-red-400 text-2xl"></i>
          </div>
          <h3 className="text-xl font-medium text-white mb-2">Unable to Load Secrets</h3>
          <p className="text-white/60 max-w-md mx-auto">Failed to load secrets. Please try again later or refresh the page.</p>
          <button className="mt-6 px-6 py-2 border border-white/20 rounded-full text-white/80 hover:text-white hover:border-white/40 transition-colors">
            Try Again
          </button>
        </div>
      </section>
    );
  }
  // Empty state
  if (secrets.length === 0) {
    return (
      <section className="relative">
        <div className="relative mb-10">
          <h2 className="font-['Playfair_Display'] font-bold text-3xl text-white relative inline-block">
            Inner Wisdom Shared
          </h2>
          <div className="absolute -bottom-3 left-0 w-24 h-1 bg-[#ff5e00] rounded-full"></div>
        </div>
        
        <div className="bg-black/40 backdrop-blur-sm rounded-lg p-12 text-center shadow-[0_15px_40px_rgba(0,0,0,0.3)] border border-white/5">
          <div className="inline-flex items-center justify-center w-20 h-20 rounded-full bg-black/50 border border-white/10 mb-6">
            <i className="ri-quill-pen-line text-white/60 text-2xl"></i>
          </div>
          <h3 className="text-xl font-medium text-white mb-2">No Secrets Yet</h3>
          <p className="text-white/60 max-w-md mx-auto">No secrets have been shared yet. Be the first to share your inner wisdom!</p>
          <button className="mt-6 px-6 py-2 border border-[#ff5e00] rounded-full text-white/90 hover:text-white transition-colors group">
            <span className="flex items-center space-x-1">
              <span>Share Now</span>
              <span className="group-hover:translate-x-1 transition-transform duration-300 text-[#ff5e00]">→</span>
            </span>
          </button>
        </div>
      </section>
    );
  }
  // Secrets list
  return (
    <section className="relative">
      <div className="relative mb-10">
        <h2 className="font-['Playfair_Display'] font-bold text-3xl text-white relative inline-block">
          Inner Wisdom Shared
        </h2>
        <div className="absolute -bottom-3 left-0 w-24 h-1 bg-[#ff5e00] rounded-full"></div>
      </div>
      
      <div className="space-y-8">
        {secrets.map((secret) => (
          <SecretItem key={secret.id} secret={secret} />
        ))}
      </div>
      
      {/* Load more button like Idliez */}
      <div className="flex justify-center mt-12">
        <button className="px-8 py-3 border border-white/10 rounded-full text-white/70 hover:text-white hover:border-white/30 transition-all duration-300 flex items-center space-x-2 group">
          <span>Load More</span>
          <span className="group-hover:translate-y-1 transition-transform duration-300">↓</span>
        </button>
      </div>
    </section>
  );
};
/* FILE: client/src/index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply font-sans antialiased bg-background text-foreground;
  }
  /* Elegant page transitions */
  a, button {
    @apply transition-all duration-300;
  }
}
/* Custom animations for enhanced aesthetics */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fadeIn {
  animation: fadeIn 0.8s ease-out forwards;
}
@keyframes fadeInLeft {
  from { opacity: 0; transform: translateX(-20px); }
  to { opacity: 1; transform: translateX(0); }
}
.animate-fadeInLeft {
  animation: fadeInLeft 0.8s ease-out forwards;
}
@keyframes fadeInRight {
  from { opacity: 0; transform: translateX(20px); }
  to { opacity: 1; transform: translateX(0); }
}
.animate-fadeInRight {
  animation: fadeInRight 0.8s ease-out forwards;
}
@keyframes pulse {
  0% { opacity: 0.5; }
  50% { opacity: 0.8; }
  100% { opacity: 0.5; }
}
.animate-pulse {
  animation: pulse 8s ease-in-out infinite;
}
@keyframes float {
  0% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
  100% { transform: translateY(0px); }
}
.animate-float {
  animation: float 6s ease-in-out infinite;
}
/* Custom styling for scrollbars */
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}
::-webkit-scrollbar-track {
  background: rgba(0, 0, 0, 0.1);
}
::-webkit-scrollbar-thumb {
  background: rgba(255, 94, 0, 0.2);
  border-radius: 4px;
}
::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 94, 0, 0.4);
}
// FILE: server/routes.ts
import type { Express } from "express";
import { createServer, type Server } from "http";
import { storage } from "./storage";
import { insertSecretSchema } from "@shared/schema";
import { fromZodError } from "zod-validation-error";
export async function registerRoutes(app: Express): Promise<Server> {
  // put application routes here
  // prefix all routes with /api
  // Get all secrets
  app.get("/api/secrets", async (req, res) => {
    try {
      const secrets = await storage.getAllSecrets();
      res.json(secrets);
    } catch (error) {
      console.error("Error getting secrets:", error);
      res.status(500).json({ message: "Failed to retrieve secrets" });
    }
  });
  // Create a new secret
  app.post("/api/secrets", async (req, res) => {
    try {
      const parsedBody = insertSecretSchema.safeParse(req.body);
      
      if (!parsedBody.success) {
        const errorMessage = fromZodError(parsedBody.error).message;
        return res.status(400).json({ message: errorMessage });
      }
      
      const secret = await storage.createSecret(parsedBody.data);
      res.status(201).json(secret);
    } catch (error) {
      console.error("Error creating secret:", error);
      res.status(500).json({ message: "Failed to create secret" });
    }
  });
  // Like a secret
  app.post("/api/secrets/:id/like", async (req, res) => {
    try {
      const id = parseInt(req.params.id, 10);
      if (isNaN(id)) {
        return res.status(400).json({ message: "Invalid secret ID" });
      }
      
      const updatedSecret = await storage.likeSecret(id);
      if (!updatedSecret) {
        return res.status(404).json({ message: "Secret not found" });
      }
      
      res.json(updatedSecret);
    } catch (error) {
      console.error("Error liking secret:", error);
      res.status(500).json({ message: "Failed to like secret" });
    }
  });
  const httpServer = createServer(app);
  return httpServer;
}
// FILE: server/storage.ts
import { users, type User, type InsertUser, secrets, type Secret, type InsertSecret } from "@shared/schema";
// modify the interface with any CRUD methods
// you might need
export interface IStorage {
  getUser(id: number): Promise<User | undefined>;
  getUserByUsername(username: string): Promise<User | undefined>;
  createUser(user: InsertUser): Promise<User>;
  getAllSecrets(): Promise<Secret[]>;
  getSecret(id: number): Promise<Secret | undefined>;
  createSecret(secret: InsertSecret): Promise<Secret>;
  likeSecret(id: number): Promise<Secret | undefined>;
}
export class MemStorage implements IStorage {
  private users: Map<number, User>;
  private secrets: Map<number, Secret>;
  private userCurrentId: number;
  private secretCurrentId: number;
  constructor() {
    this.users = new Map();
    this.secrets = new Map();
    this.userCurrentId = 1;
    this.secretCurrentId = 1;
  }
  async getUser(id: number): Promise<User | undefined> {
    return this.users.get(id);
  }
  async getUserByUsername(username: string): Promise<User | undefined> {
    return Array.from(this.users.values()).find(
      (user) => user.username === username,
    );
  }
  async createUser(insertUser: InsertUser): Promise<User> {
    const id = this.userCurrentId++;
    const user: User = { ...insertUser, id };
    this.users.set(id, user);
    return user;
  }
  async getAllSecrets(): Promise<Secret[]> {
    return Array.from(this.secrets.values()).sort((a, b) => {
      return new Date(b.timestamp).getTime() - new Date(a.timestamp).getTime();
    });
  }
  async getSecret(id: number): Promise<Secret | undefined> {
    return this.secrets.get(id);
  }
  async createSecret(insertSecret: InsertSecret): Promise<Secret> {
    const id = this.secretCurrentId++;
    const timestamp = new Date();
    const secret: Secret = { 
      ...insertSecret, 
      id, 
      likes: 0, 
      timestamp 
    };
    this.secrets.set(id, secret);
    return secret;
  }
  async likeSecret(id: number): Promise<Secret | undefined> {
    const secret = this.secrets.get(id);
    if (secret) {
      const updatedSecret = { ...secret, likes: secret.likes + 1 };
      this.secrets.set(id, updatedSecret);
      return updatedSecret;
    }
    return undefined;
  }
}
export const storage = new MemStorage();
