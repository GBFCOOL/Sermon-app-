// Load saved sermon + query
useEffect(() => {
  const saved = localStorage.getItem("sermons");
  const savedId = localStorage.getItem("selectedSermon");
  const savedQuery = localStorage.getItem("query");

  if (saved) {
    const parsed = JSON.parse(saved);
    setSermons(parsed);
    const match = parsed.find(s => s.id === Number(savedId)) || parsed[0];
    setSelected(match);
  } else {
    resetSermons();
  }

  if (savedQuery) {
    setQuery(savedQuery);
    fetchScripture(savedQuery);
  }
}, []);

// Save on changes
useEffect(() => {
  if (selected) localStorage.setItem("selectedSermon", selected.id);
}, [selected]);

useEffect(() => {
  if (query) localStorage.setItem("query", query);
}, [query]);
