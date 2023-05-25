n = [int(input("Numarul de virfuri: ")), int(input("Numarul muchiilor: "))]
k = int(input("Lungimea traseului: "))
i = int(input("Start: "))
h = int(input("Finish: "))

print("Virfurile intre care sunt muchii si ponderea lor:\nExemplu: m[1] 1 2 10")
m = []
for _ in range(n[1]):
    m.append([int(x) for x in input("m[" + str(_ + 1) + "] ").split()])

l = [[] for _ in range(n[0])]
for j in range(n[1]):
    l[m[j][0] - 1].append(m[j])

def graf(l, i, k, h, d=[]):
    if len(d) == k:
        if d[-1][1] == h:
            return [d]
        else:
            return []
    r = []
    for f in l[i - 1]:
        r.extend(graf(l, f[1], k, h, d + [f]))
    return r

print("Solutii:")
st = []
r = graf(l, i, k, h)
print(r)

for x in r:
    s = 0
    print("{" + str(x[0][0]), end='')
    for y in x:
        s += y[2]
        print(", " + str(y[1]), end='')
    print("} pondere: " + str(s))
    st.append(s)

print("Solutia cu cea mai mica pondere:\n{" + str(r[st.index(min(st))][0][0]), end='')
for y in r[st.index(min(st))]:
    print(", " + str(y[1]), end='')
print("} pondere: " + str(min(st)))

print(", " + str(y[1]), end='')
print("} pondere: " + str(min(st)))
