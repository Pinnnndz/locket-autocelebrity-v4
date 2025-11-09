import React, { useState, useEffect, useRef } from 'react';

// Declare marked and lucide to be available globally from the CDN script
declare global {
  interface Window {
    marked: {
      parse: (markdown: string) => string;
    };
    lucide: {
      createIcons: () => void;
    };
  }
}

const readmeContent = `
<h2 id="introduction" class="scroll-mt-24">🚀 Kỷ Nguyên Mới Của Tự Động Hóa</h2>
<p class="text-lg text-gray-300 mt-4">
  <strong>Locket Pro Automation</strong> không phải là một công cụ. Đây là <strong>trợ lý ảo</strong> của bạn, được thiết kế để giải phóng bạn khỏi những tác vụ lặp đi lặp lại nhàm chán. Hãy quên đi việc click chuột thủ công. Chào mừng bạn đến với hiệu suất tối đa.
</p>

<div class="my-12 border-t border-purple-900/50"></div>

<h2 id="features" class="scroll-mt-24">✨ Bộ Công Cụ Tính Năng</h2>
<div class="grid md:grid-cols-2 gap-6 mt-6">
  <div class="bg-gray-800/50 p-6 rounded-lg border border-gray-700 backdrop-blur-sm">
    <h3 class="font-semibold text-xl text-purple-400 mb-2">⚡️ Kích Hoạt Siêu Tốc</h3>
    <p class="text-gray-400">Một cú nhấp chuột duy nhất để khởi động toàn bộ chuỗi tác vụ. Tiết kiệm thời gian, tối ưu hóa năng suất.</p>
  </div>
  <div class="bg-gray-800/50 p-6 rounded-lg border border-gray-700 backdrop-blur-sm">
    <h3 class="font-semibold text-xl text-purple-400 mb-2">🛡️ Pháo Đài Bảo Mật</h3>
    <p class="text-gray-400">Hoạt động trong môi trường Tampermonkey, không yêu cầu mật khẩu hay truy cập dữ liệu cá nhân. An toàn tuyệt đối.</p>
  </div>
  <div class="bg-gray-800/50 p-6 rounded-lg border border-gray-700 backdrop-blur-sm">
    <h3 class="font-semibold text-xl text-purple-400 mb-2">🎨 Giao Diện Trực Quan</h3>
    <p class="text-gray-400">Bảng điều khiển tinh gọn, tự động ghim vào góc màn hình, giúp bạn dễ dàng kiểm soát mà không làm gián đoạn công việc.</p>
  </div>
  <div class="bg-gray-800/50 p-6 rounded-lg border border-gray-700 backdrop-blur-sm">
    <h3 class="font-semibold text-xl text-purple-400 mb-2">🌐 Tương Thích Đa Nền Tảng</h3>
    <p class="text-gray-400">Hoạt động mượt mà trên PC (Chrome, Edge, Firefox) và Mobile (Kiwi Browser). Trải nghiệm đồng nhất.</p>
  </div>
</div>

<div class="my-12 border-t border-purple-900/50"></div>

<h2 id="installation" class="scroll-mt-24">🛠️ Quy Trình Triển Khai: 3 Bước Đơn Giản</h2>
<ol class="relative border-l border-gray-700 space-y-10 ml-4 mt-6">
    <li class="ml-8">
        <span class="absolute flex items-center justify-center w-8 h-8 bg-purple-900 rounded-full -left-4 ring-4 ring-gray-900/50 text-purple-300 font-bold">1</span>
        <h3 class="font-semibold text-xl text-white">Cài Đặt Tampermonkey</h3>
        <p class="text-gray-400">Nền tảng "bệ phóng" không thể thiếu. Nếu đã có, bỏ qua bước này.</p>
        <a href="https://www.tampermonkey.net/" target="_blank" rel="noopener noreferrer" class="inline-flex items-center text-purple-400 hover:text-purple-300 mt-2">Tải về cho trình duyệt <i data-lucide="arrow-right" class="w-4 h-4 ml-1"></i></a>
    </li>
    <li class="ml-8">
        <span class="absolute flex items-center justify-center w-8 h-8 bg-purple-900 rounded-full -left-4 ring-4 ring-gray-900/50 text-purple-300 font-bold">2</span>
        <h3 class="font-semibold text-xl text-white">Cài Đặt Locket Pro Script</h3>
        <p class="text-gray-400">Click vào nút bên dưới và nhấn "Install".</p>
        <a href="https://raw.githubusercontent.com/Pinnnndz/locket-autocelebrity-v4/main/tampermonkey.user.js" class="inline-block mt-4 bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-6 rounded-lg transition-transform transform hover:scale-105">Cài Đặt Script</a>
    </li>
    <li class="ml-8">
        <span class="absolute flex items-center justify-center w-8 h-8 bg-purple-900 rounded-full -left-4 ring-4 ring-gray-900/50 text-purple-300 font-bold">3</span>
        <h3 class="font-semibold text-xl text-white">Khởi Động & Tận Hưởng</h3>
        <p class="text-gray-400">Truy cập <a href="https://locket.binhake.dev/" target="_blank" rel="noopener noreferrer" class="text-purple-400 hover:underline">Locketbinhake</a>, bảng điều khiển sẽ tự động xuất hiện. Nhấn "Bắt đầu" và xem phép màu xảy ra.</p>
    </li>
</ol>

<div class="my-12 border-t border-purple-900/50"></div>

<h2 id="faq" class="scroll-mt-24">🚨 Gặp Sự Cố?</h2>
<div class="space-y-4 mt-6">
    <details class="group bg-gray-800/50 border border-gray-700 rounded-lg p-4 backdrop-blur-sm">
        <summary class="flex items-center justify-between cursor-pointer font-semibold text-white">
            Bảng điều khiển không xuất hiện
            <i data-lucide="chevron-down" class="w-5 h-5 transition-transform duration-300 group-open:rotate-180"></i>
        </summary>
        <div class="mt-4 text-gray-400 prose prose-invert prose-a:text-purple-400">
            <p><strong>Chẩn đoán:</strong> 99% do Tampermonkey chưa được cấp quyền hoạt động đầy đủ.</p>
            <p><strong>Giải pháp:</strong> Vào <code>chrome://extensions</code>, tìm Tampermonkey và đảm bảo các quyền cần thiết đã được <strong>BẬT</strong>, sau đó tải lại trang (F5).</p>
        </div>
    </details>
    <details class="group bg-gray-800/50 border border-gray-700 rounded-lg p-4 backdrop-blur-sm">
        <summary class="flex items-center justify-between cursor-pointer font-semibold text-white">
            Trang web bị treo hoặc dính Captcha
            <i data-lucide="chevron-down" class="w-5 h-5 transition-transform duration-300 group-open:rotate-180"></i>
        </summary>
        <div class="mt-4 text-gray-400 prose prose-invert prose-a:text-purple-400">
             <p><strong>Chẩn đoán:</strong> Website có thể chặn IP từ nước ngoài.</p>
             <p><strong>Giải pháp:</strong> Sử dụng VPN và chuyển vùng về <strong>Việt Nam</strong>. Đề xuất: <a href="https://chromewebstore.google.com/detail/urban-vpn-proxy/eppiocemhmnlbhjplcgkofciiegomcon?hl=vi" target="_blank" rel="noopener noreferrer">Urban VPN</a>.</p>
        </div>
    </details>
</div>

<div class="my-12 border-t border-purple-900/50"></div>

<h2 id="contribute" class="scroll-mt-24">🤝 Tham Gia & Đóng Góp</h2>
<p class="text-gray-300 mt-4">
    <strong>Locket Pro</strong> được xây dựng bởi cộng đồng. Mọi ý tưởng, báo cáo lỗi, và đóng góp đều là nguồn động lực vô giá. Gặp vấn đề? Hãy liên hệ trực tiếp qua Facebook.
</p>
<a href="https://www.facebook.com/hphuoc.2007" target="_blank" rel="noopener noreferrer" class="inline-flex items-center justify-center gap-2 bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-lg transition-transform transform hover:scale-105 mt-4">
    <i data-lucide="message-square"></i>
    Liên Hệ Tác Giả
</a>
`;

const headings = [
  { id: 'introduction', title: 'Giới Thiệu' },
  { id: 'features', title: 'Tính Năng' },
  { id: 'installation', title: 'Cài Đặt' },
  { id: 'faq', title: 'Hỏi Đáp' },
  { id: 'contribute', title: 'Đóng Góp' },
];

const Hero = () => {
    const [subtitle, setSubtitle] = useState('');
    const fullSubtitle = "Giải pháp tự động hóa thế hệ mới cho Locketbinhake.";

    useEffect(() => {
        let i = 0;
        const typingInterval = setInterval(() => {
            if (i < fullSubtitle.length) {
                setSubtitle(prev => prev + fullSubtitle.charAt(i));
                i++;
            } else {
                clearInterval(typingInterval);
            }
        }, 50);
        return () => clearInterval(typingInterval);
    }, []);


    return (
        <div className="text-center py-20 px-4">
            <h1 className="text-5xl md:text-7xl font-extrabold tracking-tight mb-4">
                <span className="bg-clip-text text-transparent bg-gradient-to-r from-purple-400 to-pink-500">
                    Locket Pro Automation
                </span>
            </h1>
            <p className="text-xl md:text-2xl text-gray-300 max-w-3xl mx-auto h-8">
                {subtitle}
                <span className="animate-ping">_</span>
            </p>
             <a href="https://raw.githubusercontent.com/Pinnnndz/locket-autocelebrity-v4/main/tampermonkey.user.js" className="mt-10 inline-block bg-purple-600 hover:bg-purple-700 text-white font-bold py-4 px-10 rounded-full transition-all duration-300 transform hover:scale-110 shadow-lg shadow-purple-500/40 text-lg">
                Triển Khai Ngay
             </a>
        </div>
    )
}

const App: React.FC = () => {
  const [htmlContent, setHtmlContent] = useState('');
  const [activeId, setActiveId] = useState(headings[0].id);
  const observer = useRef<IntersectionObserver | null>(null);

  useEffect(() => {
    if (window.marked) {
      // Use a timeout to ensure the DOM is ready for Lucide
      setTimeout(() => {
        setHtmlContent(window.marked.parse(readmeContent));
      }, 0);
    }
  }, []);
  
  useEffect(() => {
    if (htmlContent && window.lucide) {
        window.lucide.createIcons();
        
        const sectionObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('is-visible');
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('.fade-in-section > *').forEach(el => {
            sectionObserver.observe(el as HTMLElement);
        });

        return () => sectionObserver.disconnect();
    }
  }, [htmlContent]);

  useEffect(() => {
    const handleObserver = (entries: IntersectionObserverEntry[]) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
            setActiveId(entry.target.id);
        }
      });
    };
    
    observer.current = new IntersectionObserver(handleObserver, {
        rootMargin: "-20% 0px -80% 0px"
    });

    const elements = document.querySelectorAll("h2[id]");
    elements.forEach(elem => observer.current?.observe(elem));

    return () => observer.current?.disconnect();
  }, [htmlContent]);


  return (
    <div className="min-h-screen bg-transparent font-sans p-4 sm:p-6 lg:p-8">
        <Hero />
        <div className="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 gap-12">
            <aside className="hidden lg:block lg:col-span-3 sticky top-24 self-start">
                <nav className="space-y-2">
                    <p className="font-bold text-gray-400 text-sm uppercase tracking-wider">Nội dung</p>
                    {headings.map(heading => (
                        <a 
                            key={heading.id}
                            href={`#${heading.id}`} 
                            className={`block font-medium rounded-md transition-all duration-200 py-2 px-3 ${activeId === heading.id ? 'bg-purple-500/20 text-purple-300' : 'text-gray-400 hover:bg-gray-700/50 hover:text-white'}`}
                        >
                            {heading.title}
                        </a>
                    ))}
                </nav>
            </aside>
            <main className="lg:col-span-9">
                <div className="bg-gray-900/50 backdrop-blur-xl rounded-lg shadow-2xl overflow-hidden border border-gray-700/50">
                    <article
                        className="p-6 sm:p-10 text-gray-300 fade-in-section space-y-8"
                        dangerouslySetInnerHTML={{ __html: htmlContent }}
                    />
                </div>
            </main>
        </div>
        <footer className="text-center py-12 text-gray-500">
            <p>Rendered with React, Tailwind CSS, and Framer Motion</p>
        </footer>
    </div>
  );
};

export default App;
