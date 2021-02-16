# lru-cache

const cache = (cacheSize) => {
    const hashmap = {}
    let lru = []

    function set(key, value) {
        if(lru.length == cacheSize) {
            const key = lru.shift()
            delete hashmap[key]
        }
        lru.push(key);
        return hashmap[key] = {value}
    }

    function get(key) {
        const keyIndex = lru.findIndex(key) // funcao q retorna index do array
        const leftPart = [...lru].slice(0, keyIndex)
        const rightPart = [...lru].slice(keyIndex, lru.length)
        lru = [leftPart, rightPart, lru[keyIndex]]
        return hashmap[key] ? hashmap[key] : -1
    }

    return {
        get,
        set
    }
}
const cache = cache(2);
