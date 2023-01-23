<template>
  <div class="container">
    <h1>Add Favourite Book</h1>
    <form id="book-form">
      <div>
        <label for="#">Title</label>
        <input
          type="text"
          id="bookName"
          class="u-full-width"
          placeholder="Book Name"
          v-model="bookName"
        />
      </div>
      <div>
        <label for="author">Author</label>
        <input
          type="text"
          id="author"
          class="u-full-width"
          placeholder="Author Name"
          v-model="author"
        />
      </div>
      <div>
        <label for="isbn">Released</label>
        <input
          type="text"
          id="isbn"
          class="u-full-width"
          placeholder="Released date "
          v-model="released"
        />
      </div>
      <div>
        <div v-if="!isediting">
          <div v-if="!isvisible">
            <button
              :disabled="!isComplete"
              type="submit"
              value="Add In Your List"
              class="u-full-width submit"
              id="myBtn"
              @click.prevent="addItem"
            >
              Add To List
            </button>
          </div>
          <div v-else class="visible">Adding...</div>
        </div>
        <div v-else>
          <div v-if="!isvisible">
            <button
              :disabled="!isComplete"
              type="submit"
              value="Add In Your List"
              class="u-full-width submit"
              id="myBtn"
              @click.prevent="update"
            >
              Update
            </button>
          </div>
          <div v-else class="visible">Updating...</div>
        </div>
      </div>
    </form>
    <span v-if="isSubmitting">Submitting...</span>
    <table>
      <tr class="tr">
        <th>Book</th>
        <th>Author</th>
        <th>Released</th>
        <th>Update</th>
        <th>Delete</th>
      </tr>

      <tr v-for="item in items" :key="item.id" class="userItem">
        <td>{{ item.bookName }}</td>
        <td>{{ item.author }}</td>
        <td>{{ item.released }}</td>
        <td>
          <button class="btn">
            <img
              @click="updateUser(item.id, item)"
              src="~/assets/image/icons8-pencil-24.png"
              alt=""
            />
          </button>
        </td>
        <td>
          <div v-if="!isvisibles">
            <button class="btn">
              <svg
                @click="deleteItem(item.id)"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 50 50"
                width="40px"
                height="30px"
              >
                <path
                  d="M 21 0 C 19.355469 0 18 1.355469 18 3 L 18 5 L 10.1875 5 C 10.0625 4.976563 9.9375 4.976563 9.8125 5 L 8 5 C 7.96875 5 7.9375 5 7.90625 5 C 7.355469 5.027344 6.925781 5.496094 6.953125 6.046875 C 6.980469 6.597656 7.449219 7.027344 8 7 L 9.09375 7 L 12.6875 47.5 C 12.8125 48.898438 14.003906 50 15.40625 50 L 34.59375 50 C 35.996094 50 37.1875 48.898438 37.3125 47.5 L 40.90625 7 L 42 7 C 42.359375 7.003906 42.695313 6.816406 42.878906 6.503906 C 43.058594 6.191406 43.058594 5.808594 42.878906 5.496094 C 42.695313 5.183594 42.359375 4.996094 42 5 L 32 5 L 32 3 C 32 1.355469 30.644531 0 29 0 Z M 21 2 L 29 2 C 29.5625 2 30 2.4375 30 3 L 30 5 L 20 5 L 20 3 C 20 2.4375 20.4375 2 21 2 Z M 11.09375 7 L 38.90625 7 L 35.3125 47.34375 C 35.28125 47.691406 34.910156 48 34.59375 48 L 15.40625 48 C 15.089844 48 14.71875 47.691406 14.6875 47.34375 Z M 18.90625 9.96875 C 18.863281 9.976563 18.820313 9.988281 18.78125 10 C 18.316406 10.105469 17.988281 10.523438 18 11 L 18 44 C 17.996094 44.359375 18.183594 44.695313 18.496094 44.878906 C 18.808594 45.058594 19.191406 45.058594 19.503906 44.878906 C 19.816406 44.695313 20.003906 44.359375 20 44 L 20 11 C 20.011719 10.710938 19.894531 10.433594 19.6875 10.238281 C 19.476563 10.039063 19.191406 9.941406 18.90625 9.96875 Z M 24.90625 9.96875 C 24.863281 9.976563 24.820313 9.988281 24.78125 10 C 24.316406 10.105469 23.988281 10.523438 24 11 L 24 44 C 23.996094 44.359375 24.183594 44.695313 24.496094 44.878906 C 24.808594 45.058594 25.191406 45.058594 25.503906 44.878906 C 25.816406 44.695313 26.003906 44.359375 26 44 L 26 11 C 26.011719 10.710938 25.894531 10.433594 25.6875 10.238281 C 25.476563 10.039063 25.191406 9.941406 24.90625 9.96875 Z M 30.90625 9.96875 C 30.863281 9.976563 30.820313 9.988281 30.78125 10 C 30.316406 10.105469 29.988281 10.523438 30 11 L 30 44 C 29.996094 44.359375 30.183594 44.695313 30.496094 44.878906 C 30.808594 45.058594 31.191406 45.058594 31.503906 44.878906 C 31.816406 44.695313 32.003906 44.359375 32 44 L 32 11 C 32.011719 10.710938 31.894531 10.433594 31.6875 10.238281 C 31.476563 10.039063 31.191406 9.941406 30.90625 9.96875 Z"
                />
              </svg>
            </button>
          </div>
          <div v-else>deleting...</div>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "IndexPage",
  data() {
    return {
      items: [],
      bookName: "",
      author: "",
      released: "",
      selectIndex: null,
      isSubmitting: false,
      isediting: false,
      isvisible: false,
      isvisibles: false,
    };
  },
  computed: {
    isComplete() {
      return this.bookName !== "" && this.author !== "" && this.released !== "";
    },
  },
  methods: {
    async getData() {
      try {
        const { data } = await axios.get(
          "https://zany-rose-alligator-yoke.cyclic.app/todo/all"
        );
        this.items = data.todos;
      } catch (error) {}
    },
    async addItem() {
      this.isvisible = true;
      this.isSubmitting = true;
      try {
        await axios.post("https://zany-rose-alligator-yoke.cyclic.app/todo", {
          bookName: this.bookName,
          author: this.author,
          released: this.released,
        });
        // this.items = res;
        this.items.push({
          bookName: this.bookName,
          author: this.author,
          released: this.released,
        });
        this.getData();
        (this.bookName = ""), (this.author = ""), (this.released = "");
      } catch (error) {
        console.log(error);
      } finally {
        this.isvisible = false;
        this.isSubmitting = false;
      }
    },

    async deleteItem(id) {
      try {
        await axios.delete(
          ` https://zany-rose-alligator-yoke.cyclic.app/todo/${id}`
        );

        this.items = this.items.filter((el) => el.id !== id);
      } catch (error) {
        console.log(error);
      }
    },
    async updateUser(id, item) {
      console.log("Test", id, item);
      this.bookName = item.bookName;
      this.author = item.author;
      this.released = item.released;
      this.selectIndex = id;
      this.isediting = true;
      console.log("Index Number", id, item);
    },
    async update() {
      console.log("Find Index Number", this.selectIndex);
      this.isvisible = true;
      try {
        await axios.put(
          `https://zany-rose-alligator-yoke.cyclic.app/todo/${this.selectIndex}`,
          {
            bookName: this.bookName,
            author: this.author,
            released: this.released,
          }
        );
      } catch (erro) {
        console.log(erro);
      } finally {
        this.isediting = false;
        this.isvisible = false;
        this.getData();
      }
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
.container {
  padding: 2rem;
  margin: auto;
  max-width: 1200px;
}
.container h1 {
  font-size: 2.5rem;
  padding: 1rem 0;
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(59, 76, 124);
}
#book-form input {
  width: 100%;
  margin-bottom: 1rem;
  padding: 0.7rem 1rem;
  outline: none;
  border: 1px solid rgb(20, 116, 70);
  font-size: 1rem;
  border-radius: 5px;
}
.btn {
  outline: none;
  border: none;
  background: transparent;
  cursor: pointer;
}
#myBtn:disabled {
  cursor: not-allowed;
  opacity: 0.8;
}
#book-form input::placeholder {
  font-family: Arial, Helvetica, sans-serif;
}

.submit {
  width: 100%;
  margin-bottom: 1rem;
  padding: 0.7rem 1rem;
  outline: none;
  border: none !important;
  color: #fff;
  background: #5ac6f8;
  font-size: 1.3rem !important;
  font-family: Arial, Helvetica, sans-serif;
  cursor: pointer;
}
.visible {
  width: 100%;
  margin-bottom: 1rem;
  padding: 0.7rem 1rem;
  text-align: center;
  outline: none;
  border: none !important;
  color: #fff;
  background: #5ac6f8;
  font-size: 1.3rem !important;
  font-family: Arial, Helvetica, sans-serif;
  cursor: pointer;
}
label {
  display: block;
  font-family: "Gill Sans", sans-serif;
  margin-bottom: 0.5rem !important;
  font-size: 1.4rem;
  font-weight: 500;
}
.loader-del {
  width: 70px;
  height: 70px;
}
table {
  width: 100%;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
.userItem td {
  font-family: "Gill Sans", sans-serif;
  font-size: 1.1rem;
  font-weight: 500;
}

td,
th {
  text-align: left;
  padding: 0.8rem !important;
}
tr {
  border-bottom: 1px solid rgb(46, 46, 152);
}
.tr {
  background: #219ebc;
  color: white;
  border: none !important;
}
tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
