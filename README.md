// Inside main accept loop:
int *new_sock = malloc(sizeof(int));
if (new_sock == NULL) {
    perror("malloc failed");
    close(new_socket);
    continue;
}
*new_sock = new_socket;

if (pthread_create(&thread_id, NULL, handle_connection, (void *)new_sock) < 0) {
    perror("could not create thread");
    free(new_sock);
    close(new_socket);
    continue;
}
pthread_detach(thread_id);

// Inside handle_connection(void *socket_desc):
void *handle_connection(void *socket_desc) {
    int sock = *(int *)socket_desc;
    free(socket_desc); // Free allocated int

    // ... process socket data ...

    close(sock); // Clean up connection
    return NULL;
}
