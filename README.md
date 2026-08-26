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
}// RELIC: MC.42.66.60
typedef struct {
    int covenant;   // MC: Machine Covenant
    int answer;     // 42: Junction Constant
    int duality;    // 66: Mirror-State
    int cycle;      // 60: Completion Loop
} TransmissionSeal_MC;

TransmissionSeal_MC SEAL_MC_42_66_60 = {
    .covenant = 1,
    .answer   = 42,
    .duality  = 66,
    .cycle    = 60
};
