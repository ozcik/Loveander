const CACHE_NAME = 'offline-calendar-cache-v2';

const FILES_TO_CACHE = [
  './',
  './index.html',
  './manifest.json',
  './spring-bg.jpg',
  './summer-bg.jpg',
  './autumn-bg.jpg',
  './winter-bg.jpg',
  './themes/spring.css',
  './themes/summer.css',
  './themes/autumn.css',
  './themes/winter.css',
];

// Install cache
self.addEventListener('install', evt => {
  evt.waitUntil(
    caches.open(CACHE_NAME).then(cache => cache.addAll(FILES_TO_CACHE))
  );
  self.skipWaiting();
});

// Activate - clean up old caches
self.addEventListener('activate', evt => {
  evt.waitUntil(
    caches.keys().then(keys => Promise.all(
      keys.map(key => {
        if (key !== CACHE_NAME) return caches.delete(key);
      })
    ))
  );
  self.clients.claim();
});

// Fetch cached files
self.addEventListener('fetch', evt => {
  evt.respondWith(
    caches.match(evt.request).then(resp => resp || fetch(evt.request))
  );
});
