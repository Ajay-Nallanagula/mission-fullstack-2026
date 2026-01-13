# Mission Fullstack

### Repository collection:

[Mission-Fullstack-2026](https://github.com/Ajay-Nallanagula/mission-fullstack-2026.git)

- [nextjs-practice-demos.git](https://github.com/Ajay-Nallanagula/nextjs-practice-demos.git)
- [nestjs-practice-demos.git](https://github.com/Ajay-Nallanagula/nestjs-practice-demos.git)
- [system-design-notes.git](https://github.com/Ajay-Nallanagula/system-design-notes.git)
- [react-redux-scratch-setup.git](https://github.com/Ajay-Nallanagula/react-redux-scratch-setup.git)

To add `Repo_NestedA.1` and `Repo_NestedA.2` as submodules inside `RepoA` on GitHub, follow these steps:

---

### **Step-by-Step Guide to Adding Submodules**

1. **Clone RepoA (if you haven’t already):**

   ```bash
   git clone https://github.com/Ajay-Nallanagula/mission-fullstack-2026.git
   cd mission-fullstack-2026
   ```

2. **Add Repo_NestedA.1 as a submodule:**

   ```bash
   git submodule add https://github.com/Ajay-Nallanagula/nextjs-practice-demos.git nextjs-practice-demos
   ```

3. **Add Repo_NestedA.2 as a submodule:**

   ```bash
   git submodule add https://github.com/Ajay-Nallanagula/nestjs-practice-demos.git nestjs-practice-demos
   ```

4. **Commit the changes:**
   ```bash
   git add .gitmodules nextjs-practice-demos nestjs-practice-demos
   git commit -m "Add nextjs-practice-demos and nestjs-practice-demos as submodules"
   git push
   ```

---

### **What Happens Next?**

- The folders `nextjs-practice-demos` and `nestjs-practice-demos` will appear in `RepoA`, but they are linked to their own repositories.
- When someone clones `RepoA`, they should run:
  ```bash
  git clone --recurse-submodules https://github.com/Ajay-Nallanagula/mission-fullstack-2026.git
  ```
  or, if already cloned:
  ```bash
  git submodule update --init --recursive
  ```

---

### **Notes**

- Submodules are pointers to specific commits in the child repositories.
- You can update the submodule to the latest commit by running:
  ```bash
  cd nextjs-practice-demos.git
  git pull origin main
  cd ..
  git add nextjs-practice-demos.git
  git commit -m "Update nextjs-practice-demos.git submodule"
  git push
  ```

---
